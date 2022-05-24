### Working with Processes

#### Primer

##### System calls

The kernel of your Unix system sits atop the hardware of your computer.

It’s the middle man for any interactions that need to happen with the hardware.

This include things like writing/reading from the filesystem, sending data over the network, allocating memory, or playing audio over the speakers.

Given its power, programs are not allowed direct access to the kernel. Any communication is done via system calls.

![[user application.png]]

System calls are at the heart of C programming.

System calls allow you user-space programs to interact indirectly with the hardware of your computer, via the kernel.


##### Processes: The atoms of Unix

Processes are the building block of a Unix system. Why? Because any **code that executed happens inside a process.**

One process can spawn and manage many others.

#### Processes have IDs

Every process running on your system has a unique process identifier. Hereby referred to as `pid`

```ruby
puts Process.pid
```

```shell
$ irb
2.7.2 :001 > Process.pid
 => 69625
2.7.2 :002 >
```

```shell
$ ps aux | grep irb
namtx            69633   0.0  0.0 34122844    864 s005  S+   12:55PM   0:00.01 grep --color=auto --exclude-dir=.bzr --exclude-dir=CVS --exclude-dir=.git --exclude-dir=.hg --exclude-dir=.svn --exclude-dir=.idea --exclude-dir=.tox irb
namtx            69625   0.0  0.1 34249756  22564 s002  S+   12:54PM   0:00.79 irb

```

##### Sytem calls
Ruby's `Process.pid` maps to `getpid(2)`
There is alos a global variable that holds the value of the current `pid`. You can access it with `$$`.
```shell
$ irb
2.7.2 :001 > $$
 => 69929
2.7.2 :002 >
```

#### Processes have parents
every process running on your system has a parent process. Each process knows its parent process identifier `ppid`.
In the majority of cases the parent process for a given process is the process that invoked it.

```shell
$ irb
2.7.2 :001 >
2.7.2 :001 > Process.ppid
 => 69398
2.7.2 :002 >
```

```shell
$ ps aux | grep 69398
namtx            70430   0.0  0.0 34122844    864 s003  S+    1:01PM   0:00.01 grep --color=auto --exclude-dir=.bzr --exclude-dir=CVS --exclude-dir=.git --exclude-dir=.hg --exclude-dir=.svn --exclude-dir=.idea --exclude-dir=.tox 69398
namtx            69398   0.0  0.1 34191384   8408 s005  Ss   12:54PM   0:02.76 -zsh
```

##### In the real world
There aren't a ton of uses for the `ppid` in the real world. It can be important when detecting deamon processes.

##### System calls
Ruby's `Process.ppid` maps to `getppid(2)`.

#### Processes Have File Descriptors
##### Everything is a File
A part of the Unix philosophy: in the land of Unix `everything is a file`.
This means that devices a treated as files, sockets and pipes are treated as files. and files are treated as files.

##### Descriptors represent resources
Anytime that you open a resource in a running process it is assigned a file descriptor number. File descriptors are not shared between unrelated processes, they live and die with the process they are bound to, just as any open resources for a process are close when it exits.

In Ruby, open resources are presented by the `IO` class. Any `IO` object can have an associated file descriptor number. Use `IO#fileno` to get access to it.

```ruby
passwd = File.open('/etc/passwd')
puts passwd.fileno
3
```

- File descriptor numbers are assigned the lowest unused value.
- Once a resource is closed its file descriptor number becomes available again.

File descriptors keep track of open resources only. Closed resources are not given a file descriptor number.

Trying to read file descriptor number from closed resource will raise ans exception:

```ruby
passwd = File.open('/etc/passwd')
puts passwd.fileno 
3
passwd.close 
puts passwd.fileno
-e:4:in `fileno': closed stream (IOError)
```

You may have notices that when we open a file and ask for its file descriptor number, the lowest value we get is 3. What happend to 0, 1 and 2?

##### Standard Streams
Every Unix process comes with three open resources. These are your standard input (`STDIN`), standard output (`STDOUT`) and standard error (`STDERR`) resources.

These standard resources exits for a very important reason that we take for granted today. `STDIN` provides generic way to read input from keyboard devices or pipes, `STDOUT` and `STDERR` provide generic way to write output to monitors, files, printers, etc. This was one of innovations of Unix.

```ruby
puts STDIN.fileno
0
puts STDOUT.fileno
1
puts STDERR.fileno
2
```

##### In the real world
File descriptors are at the core of network programming using sockets, pipes, etc. and are also at the core of any file system descriptors.


























