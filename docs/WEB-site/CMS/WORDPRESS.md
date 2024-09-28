## INTRO-ARCHITECT.

**WordPress** is a popular content management system ( #CMS) that allows users to create, manage, and publish content on the web. It follows a classic three-tier architecture, consisting of the following components:

1. Presentation Layer:
    
    - WordPress Themes: Themes control the visual appearance of a WordPress site. They define the layout, styling, and design elements, including colors, fonts, and page templates.
    - Templates: WordPress uses PHP-based template files to generate the HTML output for various components, such as pages, posts, archives, and more. Templates provide the structure and organization for displaying content.
    
2. Application Layer:
    
    - WordPress Core: The core software of WordPress provides the functionality and logic to manage content. It includes features like user management, content editing, database access, and more.
    - Plugins: Plugins extend the functionality of WordPress by adding new features, customizing behavior, and integrating with third-party services. Plugins can be developed by the WordPress community or created specifically for a site's requirements.
    
3. Data Layer:
    
    - Database: WordPress uses a MySQL or MariaDB database to store content, configuration settings, user information, and more. The database holds tables such as `wp_posts` for posts, `wp_users` for users, and `wp_options` for site settings.
    - Media Library: WordPress stores media files, such as images and videos, in the `wp-content/uploads` directory. Media files are associated with specific posts or pages using metadata stored in the database.

How It Works:

1. User Interaction: Users interact with the WordPress site through the front-end interface, accessing pages, posts, and other content.
2. HTTP Requests: When a user requests a WordPress page, the web server (e.g., Nginx or Apache) receives the HTTP request and forwards it to the appropriate WordPress installation.
3. WordPress Routing: WordPress parses the URL and determines the corresponding template and content to display based on the routing rules defined in the `wp-config.php` file.
4. Template Rendering: WordPress uses the chosen template file (e.g., `page.php`, `single.php`) to generate the HTML output, incorporating the necessary content from the database.
5. Database Interaction: WordPress queries the database to retrieve the content for the requested page, post, or other components. It dynamically assembles the content based on the template and user's settings.
6. Theme Rendering: The generated HTML, along with CSS styles from the active theme, is sent back to the user's browser for rendering. The browser renders the HTML and applies the CSS styles to display the web page.
7. Content Management: Administrators and editors can use the WordPress admin interface to create, edit, and manage content. The changes they make are saved in the database and reflected on the front-end of the site.

> WordPress architecture separates presentation, application, and data layers, allowing for flexible customization and content management. The combination of themes, templates, plugins, and the underlying database enables the creation of dynamic and customizable websites without the need for extensive coding knowledge.


### Is PHP-fPM In-built in Wordpress??

No, #PHP-FPM (FastCGI Process Manager) is not built into WordPress itself. PHP-FPM is a separate component of the PHP programming language that is used to manage and execute PHP scripts. It is commonly used in conjunction with web servers like Nginx or Apache to handle PHP requests.

WordPress, on the other hand, is a content management system (CMS) written in PHP. It is built to run on a web server with PHP support, but it does not include or rely on PHP-FPM by default. Instead, the choice of using PHP-FPM or any other PHP execution method is typically determined by the server configuration or the hosting environment in which WordPress is installed.

Many popular hosting providers and server setups do use #PHP-FPM to enhance the performance and scalability of WordPress websites, but it is not a core component of the WordPress software itself.