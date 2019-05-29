# 我搜集的一些编程问题

* 用牛顿法实现平方根函数

  ```text
  计算机通常使用循环来计算 x 的平方根。从某个猜测的值 z 开始，我们可以根据 z² 与 x 的近似度来调整 z，产生一个更好的猜测：z -= (z*z - x) / (2*z)
  
  重复调整的过程，猜测的结果会越来越精确，得到的答案也会尽可能接近实际的平方根。
  
  上面的 z² − x 是 z² 到它所要到达的值（即 x）的距离， 除以的 2z 为 z² 的导数，我们通过 z² 的变化速度来改变 z 的调整量。 这种通用方法叫做牛顿法。 它对很多函数，特别是平方根而言非常有效。
  ```

* 实现 `Pic`。它应当返回一个长度为 `dy` 的切片，其中每个元素是一个长度为 `dx`，元素类型为 `uint8` 的切片。当你运行此程序时，它会将每个整数解释为灰度值（好吧，其实是蓝度值）并显示它所对应的图像。

  图像的选择由你来定。几个有趣的函数包括 `(x+y)/2`, `x*y`, `x^y`, `x*log(y)` 和 `x%(y+1)`。

  （提示：需要使用循环来分配 `[][]uint8` 中的每个 `[]uint8`；请使用 `uint8(intValue)` 在类型之间转换；你可能会用到 `math` 包中的函数。）

  ```go
  package main
  
  import "golang.org/x/tour/pic"
  
  func Pic(dx, dy int) [][]uint8 {
  	// 外层slice
  	a := make([][]uint8, dy)
  	for x := range a {
  		// 里层slice
  		b := make([]uint8, dx)
  		for y := range b {
  			// 给里层slice每个元素赋值
  			b[y] = uint8(x%(y+1))
  		}
  		// 给外层slice每个元素赋值
  		a[x] = b
  	}
  	return a
  }
  
  func main() {
  	pic.Show(Pic)
  }
  ```

* 实现 `WordCount`。它应当返回一个映射，其中包含字符串 `s` 中每个“单词”的个数。函数 `wc.Test` 会对此函数执行一系列测试用例，并输出成功还是失败。

  你会发现 [strings.Fields](https://go-zh.org/pkg/strings/#Fields) 很有帮助。

  ```go
  package main
  
  import (
  	"strings"
  
  	"golang.org/x/tour/wc"
  )
  
  func WordCount(s string) map[string]int {
  	field := strings.Fields(s)
  
  	m := make(map[string]int)
  	for i := 0; i < len(field); i++ {
  		if m[field[i]] > 0 {
  			m[field[i]] = m[field[i]] + 1
  		} else {
  			m[field[i]] = 1
  		}
  	}
  	return m
  }
  
  func main() {
  	wc.Test(WordCount)
  }
  ```

* 让我们用函数做些好玩的事情。

  实现一个 `fibonacci` 函数，它返回一个函数（闭包），该闭包返回一个[斐波纳契数列](https://zh.wikipedia.org/wiki/斐波那契数列) `(0, 1, 1, 2, 3, 5, ...)`。

  ```go
  package main
  
  import "fmt"
  
  func fibonacci() func() int {
      fibItemPre1 := -1
      fibItemPre2 := 0
      fibItem := 0
  
      return func() int {
          if fibItemPre1  == -1 {
              fibItemPre1  = 0;
              return 0
          } else if fibItemPre1 == 0 {
              fibItemPre1  = 1
              return 1
          }  else {
              fibItem = fibItemPre1 + fibItemPre2
              fibItemPre2 = fibItemPre1
              fibItemPre1 = fibItem
              return fibItem
          }
      }
  }
  
  func main() {
      f := fibonacci()
      for i := 0; i < 15; i++ {
          fmt.Println(f())
      }
  }
  ```

* 练习：Stringer

  通过让 `IPAddr` 类型实现 `fmt.Stringer` 来打印点号分隔的地址。

  例如，`IPAddr{1, 2, 3, 4}` 应当打印为 `"1.2.3.4"`。
  
  ```go
  package main
  
  import "fmt"
  
  type IPAddr [4]byte
  
  // TODO: 给 IPAddr 添加一个 "String() string" 方法
  func (p IPAddr) String() string {
  	return fmt.Sprintf("%v.%v.%v.%v", p[0],p[1], p[2], p[3])
  	
  }
  
  func main() {
  	hosts := map[string]IPAddr{
  		"loopback":  {127, 0, 0, 1},
  		"googleDNS": {8, 8, 8, 8},
  	}
  	for name, ip := range hosts {
  		fmt.Printf("%v: %v\n", name, ip)
  	}
  }
  ```
  
* 练习：错误

  从[之前的练习](https://tour.go-zh.org/flowcontrol/8)中复制 `Sqrt` 函数，修改它使其返回 `error` 值。

  `Sqrt` 接受到一个负数时，应当返回一个非 nil 的错误值。复数同样也不被支持。

  创建一个新的类型

  ```
  type ErrNegativeSqrt float64
  ```

  并为其实现

  ```
  func (e ErrNegativeSqrt) Error() string
  ```

  方法使其拥有 `error` 值，通过 `ErrNegativeSqrt(-2).Error()` 调用该方法应返回 `"cannot Sqrt negative number: -2"`。

  **注意:** 在 `Error` 方法内调用 `fmt.Sprint(e)` 会让程序陷入死循环。可以通过先转换 `e` 来避免这个问题：`fmt.Sprint(float64(e))`。这是为什么呢？

  修改 `Sqrt` 函数，使其接受一个负数时，返回 `ErrNegativeSqrt` 值。
  
  ```go
  package main
  
  import (
  	"fmt"
  	"math"
  )
  
  type ErrNegativeSqrt float64
  
  func (e ErrNegativeSqrt) Error() string{
  	return fmt.Sprintf("cannot Sqrt negative number: %v", float64(e))
  }
  
  func Sqrt(x float64) (float64, error) {
  	if x < 0 {
  		return 0, ErrNegativeSqrt(x)
  	}
  	return math.Sqrt(x), nil
  }
  
  func main() {
  	fmt.Println(Sqrt(2))
  	fmt.Println(Sqrt(-2))
  }
  ```
  
* 练习：Reader

  实现一个 `Reader` 类型，它产生一个 ASCII 字符 `'A'` 的无限流。
  
  ```go
  package main
  
  import "golang.org/x/tour/reader"
  
  type MyReader struct{}
  
  // TODO: Add a Read([]byte) (int, error) method to MyReader.
  func (r MyReader) Read(b []byte) (int, error) {
      // 赋值并返回
      b[0] = 'A'
      return 1, nil
  }
  
  func main() {
  	reader.Validate(MyReader{})
  }
  ```
  
* 练习：rot13Reader

  有种常见的模式是一个 [`io.Reader`](https://go-zh.org/pkg/io/#Reader) 包装另一个 `io.Reader`，然后通过某种方式修改其数据流。

  例如，[`gzip.NewReader`](https://go-zh.org/pkg/compress/gzip/#NewReader) 函数接受一个 `io.Reader`（已压缩的数据流）并返回一个同样实现了 `io.Reader`的 `*gzip.Reader`（解压后的数据流）。

  编写一个实现了 `io.Reader` 并从另一个 `io.Reader` 中读取数据的 `rot13Reader`，通过应用 [rot13](http://en.wikipedia.org/wiki/ROT13) 代换密码对数据流进行修改。

  `rot13Reader` 类型已经提供。实现 `Read` 方法以满足 `io.Reader`。
  
  ```go
  package main
  
  import (
  	"io"
  	"os"
  	"strings"
  )
  
  type rot13Reader struct {
  	r io.Reader
  }
  
  func rot13(b byte) byte {
      switch {
      case 'A' <= b && b <= 'M':
          b = b + 13
      case 'M' < b && b <= 'Z':
          b = b - 13
      case 'a' <= b && b <= 'm':
          b = b + 13
      case 'm' < b && b <= 'z':
          b = b - 13
      }
      return b
  }
  
  func (mr rot13Reader) Read(b []byte) (int, error) {
      n, e := mr.r.Read(b)
      for i := 0; i < n; i++ {
          b[i] = rot13(b[i])
      }
      return n, e
  }
  
  func main() {
  	s := strings.NewReader("Lbh penpxrq gur pbqr!")
  	r := rot13Reader{s}
  	io.Copy(os.Stdout, &r)
  }
  ```

* 练习：等价二叉查找树

  [题目](<https://tour.go-zh.org/concurrency/7>)

* ```go
  package main
  
  import (
  	"fmt"
  
  	"golang.org/x/tour/tree"
  )
  
  // Walk 步进 tree t 将所有的值从 tree 发送到 channel ch。
  func Walk(t *tree.Tree, ch chan int) {
  	if t == nil {
  		return
  	}
  	Walk(t.Left, ch)
  	ch <- t.Value
  	Walk(t.Right, ch)
  }
  
  // Same 检测树 t1 和 t2 是否含有相同的值。
  func Same(t1, t2 *tree.Tree) bool {
  	ch1 := make(chan int)
  	ch2 := make(chan int)
  	go Walk(t1, ch1)
  	go Walk(t2, ch2)
  	for i := 0; i < 10; i++ {
  		x, y := <-ch1, <-ch2
  		fmt.Println(x, y)
  		if x != y {
  			return false
  		}
  	}
  	return true
  }
  
  func main() {
  	// fmt.Println(Same(tree.New(1), tree.New(2)))
  	fmt.Println(Same(tree.New(1), tree.New(1)))
  }
  ```

* 练习：Web 爬虫

  在这个练习中，我们将会使用 Go 的并发特性来并行化一个 Web 爬虫。

  修改 `Crawl` 函数来并行地抓取 URL，并且保证不重复。

  *提示*：你可以用一个 map 来缓存已经获取的 URL，但是要注意 map 本身并不是并发安全的！
  
  ```go
  package main
  
  import (
  	"fmt"
  	"sync"
  )
  
  type Fetcher interface {
  	Fetch(url string) (body string, urls []string, err error)
  }
  
  func Crawl(url string, depth int, fetcher Fetcher, wg *sync.WaitGroup) {
  
  	defer wg.Done()
  
  	if depth <= 0 {
  		return
  	}
  
  	if cache.has(url) {
  		// fmt.Println("already exist.")
  		return
  	}
  
  	body, urls, err := fetcher.Fetch(url)
  	if err != nil {
  		fmt.Println(err)
  		return
  	}
  
  	fmt.Printf("found: %s %q\n", url, body)
  
  	for _, u := range urls {
  		wg.Add(1)
  		go Crawl(u, depth-1, fetcher, wg)
  	}
  
  	return
  }
  
  type Cache struct {
  	cache map[string]bool
  	mutex sync.Mutex
  }
  
  func (cache *Cache) add(url string) {
  	cache.mutex.Lock()
  	cache.cache[url] = true
  	cache.mutex.Unlock()
  }
  
  func (cache *Cache) has(url string) bool {
  	cache.mutex.Lock()
  	defer cache.mutex.Unlock()
  	_, ok := cache.cache[url]
  	if !ok {
  		cache.cache[url] = true
  	}
  	return ok
  }
  
  var cache Cache = Cache{
  	cache: make(map[string]bool),
  }
  
  func main() {
  	var wg sync.WaitGroup
  
  	wg.Add(1)
  	go Crawl("https://golang.org/", 4, fetcher, &wg)
  
  	wg.Wait()
  }
  
  type fakeFetcher map[string]*fakeResult
  
  type fakeResult struct {
  	body string
  	urls []string
  }
  
  func (f fakeFetcher) Fetch(url string) (string, []string, error) {
  	if res, ok := f[url]; ok {
  		return res.body, res.urls, nil
  	}
  	return "", nil, fmt.Errorf("not found: %s", url)
  }
  
  var fetcher = fakeFetcher{
  	"https://golang.org/": &fakeResult{
  		"The Go Programming Language",
  		[]string{
  			"https://golang.org/pkg/",
  			"https://golang.org/cmd/",
  		},
  	},
  	"https://golang.org/pkg/": &fakeResult{
  		"Packages",
  		[]string{
  			"https://golang.org/",
  			"https://golang.org/cmd/",
  			"https://golang.org/pkg/fmt/",
  			"https://golang.org/pkg/os/",
  			"https://golang.org/pkg/os1/",
  		},
  	},
  	"https://golang.org/pkg/fmt/": &fakeResult{
  		"Package fmt",
  		[]string{
  			"https://golang.org/",
  			"https://golang.org/pkg/",
  		},
  	},
  	"https://golang.org/pkg/os/": &fakeResult{
  		"Package os",
  		[]string{
  			"https://golang.org/",
  			"https://golang.org/pkg/",
  		},
  	},
  }
  ```
  
  

