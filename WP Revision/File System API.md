### Why to use File System API
- You might be wondering why we don’t just use PHP’s file system functions to read and write local files instead of learning and using a whole new set of APIs?

- The issue of using PHP file system APIs is that it doesn’t take care of file permissions automatically. Suppose you’re using a shared hosting service to host your WordPress site and your hosting web server is running as the “admin” operating system account. Whenever you create files using PHP, they’re owned as the “admin” user. Therefore, any other website hosted in the same shared hosting can also access your website files as they’re also running as the “admin” user, posing a security issue to your site. To protect us from this issue, you need to change the file owner and permissions manually using PHP.

#### Creating a directory if doesn’t already exist.
```php 
if ( ! is_dir( ABSPATH . 'my-folder' ) ) {
    wp_mkdir_p( ABSPATH . 'my-folder' );
}
```
**Core Functions:**

- **WP_Filesystem()**: Initializes the filesystem and establishes a connection using the most suitable method.
- **get_filesystem_method()**: Determines the appropriate connection method based on server capabilities.
- **request_filesystem_credentials()**: Prompts the user for FTP credentials if necessary (admin area only).
- **Filesystem API functions**: Provide various functionalities for working with files and directories:
    - `put_contents()`: Write content to a file.
    - `get_contents()`: Read content from a file.
    - `rmdir()`: Delete a directory.
    - `copydir()`: Copy a directory.
    - `move_file()`: Move a file.
    - Many more for various operations.

**Benefits of using the Filesystem API:**

- **Security:** Enforces proper authentication and authorization for file operations.
- **Standardization:** Provides a consistent interface regardless of the server environment.
- **Flexibility:** Supports different connection methods for broader compatibility.
- **Code Maintainability:** Keeps code cleaner and less prone to server-specific issues.

pen_spark