

**1. Restarting a Process with Updated Environment Variables:**

* **Snippet:** `pm2 restart <process-name> --update-env`
* **Explanation:** This command restarts a specific process managed by pm2 and applies any changes made to its environment variables.  It's crucial to use this after modifying the environment file (e.g., `.env`).
* **Example:** `pm2 restart my-app --update-env` (restarts the process named "my-app")
* **Best Practice:**  Use a dedicated environment file (like `.env`) and load it in your application's startup script.  This makes environment management cleaner.

**2. Resurrecting Processes:**

* **Snippet:** `pm2 resurrect`
* **Explanation:**  This restores previously running processes based on the saved state in `dump.pm2`.  Useful after a server reboot or pm2 restart.
* **Example:** `pm2 resurrect`
* **Best Practice:** Combine this with `pm2 save` (explained below) for robust process management across restarts.

**3. Saving the Process List:**

* **Snippet:** `pm2 save`
* **Explanation:** Saves the current process list managed by pm2.  This allows pm2 to resurrect them later.
* **Example:** `pm2 save`
* **Best Practice:**  Run `pm2 save` after starting or modifying your processes to ensure the latest state is persisted.

**4. Getting Process Information:**

* **Snippet:** `pm2 info 0`
* **Snippet:** `pm2 info <process_name>`
* **Snippet:** `pm2 info <process_id>`
* **Explanation:** Displays detailed information about a specific process, identified by its ID or name.  The id '0' refers to the first process in the pm2 list
* **Example:** `pm2 info my-app` (shows info for "my-app"), `pm2 info 2` (shows info for process with ID 2)
* **Best Practice:** Use process names for clarity.  If you need the process ID, you can get it from `pm2 ls` or `pm2 jlist`.

**5. Killing a Process:**

* **Snippet:** `pm2 kill` or `pm2 kill <process_name>` or `pm2 kill <process_id>`
* **Explanation:** Kills all processes managed by pm2. For specific process use process_name or process_id
* **Example:** `pm2 kill my-app` (kills "my-app") , `pm2 kill` (kills all processes)
* **Best Practice:** For stopping a process cleanly, use `pm2 stop` instead.  `pm2 kill` is for force-stopping.

**6. Deleting a Process:**

* **Snippet:** `pm2 delete 0` or `pm2 delete <process_name>` or `pm2 delete <process_id>`
* **Explanation:** Removes a process from pm2's process list. '0' refers to the first process in the pm2 list. Use name or id for a specific process
* **Example:** `pm2 delete my-app` (removes "my-app")
* **Best Practice:**  Stop the process with `pm2 stop` before deleting it.

**7. Starting a Process:**

* **Snippet:** `pm2 start "script" --name name`
* **Explanation:** Starts a new process. The `--name` flag assigns a name to the process, which is highly recommended for easier management.  "script" can be a Node.js file, a command, or a JSON declaration file.
* **Example:** `pm2 start app.js --name my-backend` (starts `app.js` and names it "my-backend")  or `pm2 start npm -- start --name react-app`  (for starting using npm)
* **Best Practice:** Use a process file (ecosystem.config.js or a JSON file) to define your application's startup configuration for better organization and reproducibility.

**8. Viewing Logs:**

* **Snippet:** `pm2 logs 0` or `pm2 logs <process_name>` or `pm2 logs <process_id>`
* **Explanation:**  Shows the logs for a specific process. '0' refers to the first process in the pm2 list
* **Example:** `pm2 logs my-api` (shows logs for "my-api")
* **Best Practice:** Use `pm2 logrotate` regularly to manage log file sizes.

**9. Listing Processes:**

* **Snippet:** `pm2 ls` or `pm2 list`
* **Explanation:**  Displays a list of all processes managed by pm2.
* **Example:** `pm2 ls`

**10. Combined Restart and Logs:**

* **Snippet:** `pm2 restart 0 && pm2 logs 0`
* **Explanation:** Restarts a process and then immediately displays its logs.  '0' refers to the first process in the pm2 list. You can use process names or id's for specific processes
* **Example:** `pm2 restart my-app && pm2 logs my-app`
* **Best Practice:** While this works, it's generally better to restart and view logs separately for clearer debugging.


These examples and best practices will help you use pm2 more effectively to manage your Node.js applications or other processes. Remember to consult the official pm2 documentation for the most up-to-date information and advanced features.