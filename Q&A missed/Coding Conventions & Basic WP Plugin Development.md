###  Why should one use Settings API instead of settings pages?
 - The **Settings API**,  allows admin pages containing settings forms to be managed semi-automatically. 
 - It lets you define settings pages, sections within those pages and fields within the sections.
- New settings pages can be registered along with sections and fields inside them. 
- Existing settings pages can also be added to by registering new settings sections or fields inside of them.
- Settings API allows complex things to keep in order (logic is well structured), secure (nonces, validation callbacks) and extensive (hooking into another page or allowing to be hooked into).

### How WordPress handles date in different locales?
To handle date format in different locales, WordPress uses `date_i18n()` function that translates the dates into the selected language.
```php
date_i18n( 
	string $format, 
	int|bool $timestamp_with_offset = false, 
	bool $gmt = false 
)
```

```php
$localized_date = date_i18n(get_option('date_format') . ' ' . get_option('time_format'), strtotime($current_date_time))
```
- It is similar to the `date()` except that It alsp translates.
- The core of WordPress includes the necessary pieces to translate months and days and so forth in the core code, so this function is one translation function which does not need a text-domain when used in plugins and themes. The translations will always be included in the core language packs.
### What is Autoload in Options API?
In WordPress' Options API, the "autoload" parameter determines whether a specific option is loaded automatically during WordPress initialization. If an option is set to autoload, its value is retrieved from the database and made available for use without requiring an explicit request or query.

### What are the Columns postmeta table
- `meta_id`: Unique ID that is associated with postmeta field.
- `post_id`: The ID of the post that this meta field belongs to.
- `meta_key`: The key identifier for the meta term.
- `meta_value`: The actual post meta field value.
