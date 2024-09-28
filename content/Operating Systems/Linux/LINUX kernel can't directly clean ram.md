In Linux distribution, you cannot directly "clean" the RAM through a command. The Linux kernel manages RAM efficiently by dynamically allocating and freeing memory as needed. However, you can take certain actions to optimize memory usage and improve performance. Here are a few commands and techniques you can use:

1. **Clear PageCache**: The #PageCache is a mechanism used by the Linux kernel to cache files and filesystem metadata in memory. Clearing the PageCache can help free up memory. You can use the following command as the root user to clear the PageCache:   

 ``` 
 sudo echo 1 > /proc/sys/vm/drop_cache
 ```
  
2. **Clear dentries and inodes**: Dentries and inodes are other types of caches that can occupy memory. You can use the following command as the root user to clear the dentries and inodes caches:

```
sudo echo 2 > /proc/sys/vm/drop_caches 
```
   
   It's important to note that clearing caches can affect system performance, as it may result in slower file access until the caches are rebuilt. Use these commands judiciously and only when necessary.

3. **Restart services and applications**: Sometimes, certain services or applications can consume excessive memory. If you notice high memory usage by a particular process, consider restarting that process or the associated service to free up the memory it was using. Use the appropriate commands to restart the service or application, such as `systemctl restart <service-name>`.
   
4. **Check memory usage**: To monitor memory usage and identify processes that consume a significant amount of memory, you can use tools like `top`, `htop`, or `free`. These commands provide insights into memory usage by different processes and can help you identify any memory-intensive applications.


*Remember that Linux utilizes available RAM for caching and optimizing performance. It's normal to see high memory usage, as long as it is not causing performance issues or excessive swapping to disk. The Linux kernel manages memory efficiently and automatically frees up memory when needed by terminating or swapping out less-used processes.*