# Subdirectories vs Subdomains vs WordPress Multisite
It’s essential to draw a clear distinction between installing WordPress in a subdirectory, installing it on a subdomain, and installing a WordPress multisite network. Each has their own strengths, weaknesses, and applications.
### [#](https://deliciousbrains.com/move-wordpress-root-subdirectory/#subdirectories)Subdirectories

A subdirectory is a directory within the main domain, such as `yourdomain.com/blog`. They’re still part of that single website, which can make them easier to manage and optimize. In particular, a subdirectory install can be beneficial for SEO, as it inherits the authority of the main domain.

### [#](https://deliciousbrains.com/move-wordpress-root-subdirectory/#subdomains)Subdomains

A subdomain is a separate website within the same root domain, such as `blog.yourdomain.com`. Subdomains are independent entities, which can affect their SEO performance and ranking.

They also require more setup and management than subdirectories do, as each subdomain can be considered a unique site. Subdomain installs are often used to partition certain types of content or serve a particular subset of users, such as a dedicated support site, or versions of the site in other languages. One benefit of this approach is that it can help prevent your keywords from being diluted, as search engines treat them as separate sites.

### [#](https://deliciousbrains.com/move-wordpress-root-subdirectory/#wordpress-multisites)WordPress Multisites

WordPress multisite allows you to run multiple WordPress websites from one single codebase, sharing the same WordPress core, plugins, and themes across the network. All sites within the network share the same WordPress core files and are stored in the same WordPress directory.

The best technique depends heavily on the nature of your project:

- Installing WordPress in a subdirectory is useful for adding a separate website or section within your main domain.
- Installing WordPress in a subdomain is ideal for creating separate websites for different services or brands within your main domain.
- Installing WordPress in a multisite network is suitable for managing multiple websites with shared code, themes, and plugins, but with separate content and data.

## [#](https://deliciousbrains.com/move-wordpress-root-subdirectory/#determine-install-type)How to Tell if WordPress Core is Installed in a Subdirectory

![[Pasted image 20240417170230.png]]

If the values match, you have a root WordPress install. If the “WordPress Address (URL)” has an additional path compared to the “Site Address (URL),” it’s in a subdirectory. You can also tell by looking at the URL when you log into your site. If WordPress was installed in a subdirectory, then the `wp-admin` page will be shown under that subdirectory (such as `hellfish.media/wp/wp-admin/`).

