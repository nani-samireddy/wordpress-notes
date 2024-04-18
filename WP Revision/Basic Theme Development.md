## Creating Custom page templates

**Step 1: Building Your Template File**

1. **Open your text editor:** Create a new file and give it a descriptive name that reflects its purpose. For example, `page-contact.php` for a contact page template.
    
2. **Template Header:** At the beginning of the file, add a comment to tell WordPress this is a custom template:
    
    PHP
    
    ```
    <?php /* Template Name: My Contact Page Template */ ?>
    ```
    
    Replace "My Contact Page Template" with a clear name for your template.
    
3. **Template Structure:** Here's a basic layout for your template:
    
    PHP
    
    ```
    <?php
    get_header(); ?>
    
    <div id="primary" class="content-area">
        <main id="main" class="site-main">
    
            <?php
            // Your custom page content here (text, images, etc.)
            ?>
    
        </main></div>
    <?php get_footer(); ?>
    ```
    
    - `get_header()`: This retrieves your theme's header file (`header.php`).
    - `Content Area`: The `#primary` and `#main` divs hold your main content.
    - **Your Custom Content:** Replace the comment with your desired layout using HTML and basic CSS. You can also use WordPress template tags like `the_title()` to display the page title.
    - `get_footer()`: This retrieves your theme's footer file (`footer.php`).

**Step 2: Assigning the Template to a Page**

1. **Create a New Page:** In your WordPress admin panel, go to Pages > Add New.
2. **Assign the Template:** Under "Page Attributes" on the right, look for the "Template" dropdown. You should now see your custom template listed there. Select the appropriate template for the page you're creating.
3. **Publish the Page:** Once you've added your content, click "Publish" to make the page live with your custom layout!