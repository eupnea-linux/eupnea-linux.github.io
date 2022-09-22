# Crostini

## Crostini specific instructions
Due to Crostini being a bit weird, the container needs to be started with special privileges to allow for a Eupnea image creation. Follow the steps below:  
1. <kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>T</kbd>, enter `shell` and press <kbd>Enter</kbd>  

(How to run commands: Copy the ``command`` into the terminal and press <kbd>Enter</kbd>)

3. ``vmc stop termina``
4. ``vmc start termina``
5. ``vmc container termina penguin --privileged true``  

Now in the container itself run the following commands:

1. ``sudo -i``
2. ``ln -s /proc/self/fd /dev/fd``
3. ``cd /sys/fs/cgroup/``
4. Copy this whole block and paste it into the terminal, then press <kbd>Enter</kbd>: 
   ```
   if [ ! -d devices ]; then
     mkdir -p devices
     mount -t cgroup cgroup /sys/fs/cgroup/devices/ -o rw,nosuid,nodev,noexec,relatime,devices
   fi
   printf '%s\n' 'c *:* rwm' 'b *:* rwm' > devices/devices.allow
    ```
