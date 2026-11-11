```
```java
System.out.print("Enter base directory (e.g. /opt/jdk-11-src): ");
String directory = in.nextLine();
System.out.print("Enter keyword (e.g. volatile): ");
String keyword = in.nextLine();

Runnable enumerator = () -> {
    try
    {
        enumerate(Path.of(directory));
        queue.put(DUMMY);
    }
    catch (IOException e)
    {
        e.printStackTrace();
    }
    catch (InterruptedException e)
    {
    }
};

new Thread(enumerator).start();
for (int i = 1; i <= SEARCH_THREADS; i++) {
    Runnable searcher = () -> {
        try
        {
            boolean done = false;
            while (!done)
            {
                Path file = queue.take();
                if (file == DUMMY)
                {
                    queue.put(file);
                    done = true;
                }
                else search(file, keyword);
            }
        }
        catch (IOException e)
```
```