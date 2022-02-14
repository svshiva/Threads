## Welcome to Knowledge Base
## You will learn Threads in java

### Threads

Threads are sometimes called lightweight processes. Both processes and threads provide an execution environment, but creating a new thread requires fewer resources than creating a new process.

Threads exist within a process — every process has at least one. Threads share the process's resources, including memory and open files. This makes for efficient, but potentially problematic, communication.

Multithreaded execution is an essential feature of the Java platform. Every application has at least one thread — or several, if you count "system" threads that do things like memory management and signal handling. But from the application programmer's point of view, you start with just one thread, called the main thread. This thread has the ability to create additional threads, as we'll demonstrate in the next section.

### __Using Runnable Interface__

```
class Example implements Runnable {

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println("Hello from example");
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

    }

}

public class HelloRunnable implements Runnable {

    public static void main(String[] args) {
        Thread x = new Thread(new HelloRunnable());
        Thread y = new Thread(new Example());
        x.start();
        y.start();

    }

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            char x = '\u2800';
            System.out.println("Hello from run" + x);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

    }
}

```

### __Using Thread Class__

```
class A extends Thread {
    String name;

    public A(String nameString) {
        this.name = nameString;
    }

    @Override
    public void run(){
        for (int i = 0; i < 10; i++) {
            System.out.println(name);
            try {
                sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

}

public class HelloThread {
    public static void main(String[] args) {
        A a = new A("Shivam");
        A b = new A("Aditi");
        a.start();
        b.start();

    }
}
```

### Simple Thread Example

```
public class SimpleThreads {

    static void threadMessage(String message) {
        String thread_name = Thread.currentThread().getName();
        System.out.format("%s: %s,%n", thread_name, message);
    }
    
    private static class MessageLoop implements Runnable{
        @Override
        public void run() {
            String importantInfo[] = {"shivam","varnika","abhishek","aditi"};
            try{
                for (int i = 0; i < importantInfo.length; i++) {
                    Thread.sleep(2000);
                    threadMessage(importantInfo[i]);
                }
            }catch(InterruptedException e){
                threadMessage("I wasn't done yet!!!");
            }
            
        }
    }

    public static void main(String[] args) throws InterruptedException{
        long patience = 1000*60*60; // default time
        if(args.length>0){
            try{
                patience = 1000* Long.parseLong(args[0]);
            }catch(NumberFormatException e){
                System.err.println("Argument must be an integer !");
                System.exit(1);
            }
        }

        threadMessage("Starting message loop thread");
        long startTime = System.currentTimeMillis();
        Thread t = new Thread( new MessageLoop());
        t.start();
        threadMessage("Waiting for message loop thread to finish ");
        while(t.isAlive()){
            threadMessage("Still waiting");
            t.join(1000);
            if(((System.currentTimeMillis()-startTime)>patience) && t.isAlive()){
                threadMessage("Tired of waiting");
                t.interrupt();
                // Shouldn't be long now
                // -- wait indefinitely
                t.join();
            }
        }

        threadMessage("Finally!");
    }
}
```


#### Follow me on [Github](https://github.com/svshiva)