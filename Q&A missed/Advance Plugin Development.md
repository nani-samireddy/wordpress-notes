### Multi-site drop-ins
- sunrise.php
- blog-deleted.php
- blog-inactive.php
- blog-suspended.php

### brief about sunrise.php
- If SUNRISE constant is set to true, then this drop-in executed before Multisite is loaded. This drop-in loads early in the WordPress loading sequence, before mu-plugins, any active plugins, and the active theme. Because of this, what can be done in sunrise.php is limited, and confined to executing pure PHP to set constants that override WordPress Core behavior.

### Default args for HTTP request
- `timeout`: The maximum time in seconds that the request is allowed to take. Default is 5 seconds.
- `redirection`: Whether to follow redirects. Default is true, meaning redirects will be followed.
- `httpversion`: The HTTP version to use in the request. Default is '1.0'.
- `user-agent`: The user-agent header for the request. Default is 'WordPress/' followed by the WordPress version.

### How to create folder if not exists
```php
// Initialize the WordPress Filesystem
global $wp_filesystem;
if ( ! is_a( $wp_filesystem, 'WP_Filesystem_Base' ) ) {
    require_once ABSPATH . '/wp-admin/includes/file.php';
    WP_Filesystem();
}

// Define the path to the folder you want to check/create
$folder_path = WP_CONTENT_DIR . '/uploads/my-folder';

// Check if the folder exists
if ( $wp_filesystem->exists( $folder_path ) ) {
    echo 'Folder exists.';
} else {
    if ( $wp_filesystem->mkdir( $folder_path ) ) {
        echo 'Folder created successfully.';
    } else {
        echo 'Failed to create the folder.';
    }
}

```

#### Does WordPress deletes the expired transients?
Yes, WordPress infrequently cleans out expired transients. To prevent expired transients from building up in the database, it’s a good practice to always remove your transient once you are done with it and no longer need it.

[Link to the Reference ](https://arc.net/l/quote/maetpyza)

#### How to remove a Dashboard widget in WordPress
We can remove a dashboard widget in WordPress using the remove_meta_box() function. Provide the widget's ID, the dashboard screen context, and the dashboard page where you want to remove it.

```php
function remove_custom_dashboard_widget() {
    remove_meta_box('dashboard_custom_widget', 'dashboard', 'normal');
}
add_action('wp_dashboard_setup', 'remove_custom_dashboard_widget');
```

