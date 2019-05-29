# 20 Signals: Fundamental Concepts

[TOC]

## Concepts and Overview

### Signal

```markdown
A signal is a notification to a process that an event has occurred. Signals are sometimes described as *software interrupts*
```

* Each signal is defined as a unique (small) integer, starting sequentially from 1. These integers are defined in <signal.h> with symbolic names of the form SIGxxxx

* Signals fall into two broad categories:

  * the *traditional* or *standard* signals

    ```markdown
    Used by the kernel to notify processes of events. On Linux, the standard signals are numbered from 1 to 31.
    ```

  * *realtime* signals

    ```markdown
    
    ```

* **generated** , **delivered** and **pending**

  ```markdown
  A signal is said to be *generated* by some event. Once generated, a signal is later *delivered* to a process, which then takes some action in response to the signal. Between the time it is generated and the time it is delivered, a signal is said to be *pending*
  ```

  

* One process can send a signal to another process or to itself, however the usual source of many signals sent to a process is the *kernel* . Among the types of events that cause the *kernel* to generate a signal for a process are the following:

  * A hardware exception
  * The user typed one of the terminal special characters that generate signals
  * A software event occurred

### Signal mask
```markdown
A set of signals whose delivery is currently *blocked*
```

#### The default actions carried out by a process, upon delivery of a signal

* The signal is *ignored*
* The process is *terminated* (Killed)
* A *core dump file* is generated, and the process is terminated
* The process is *stopped* — execution of the process is suspended
* Execution of the process is resumed after previously being stopped

### Disposition

```markdown
Setting the *disposition* can change the action that occurs when the signal is delivered
```

* A program can set one of the following dispositions for a signal:
  * The default action should occur
  * The signal is ignored
  * A *signal handler* is executed

### Signal handler

```markdown
A signal handler is a function, written by the programmer, that performs appropriate tasks in response to the delivery of a signal
```

## Signal Types and Default Actions