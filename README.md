Traverse Child Theme
=====================

A lightweight child theme for the Traverse WordPress theme. Use this child theme to safely make customizations (styles, templates, and small PHP tweaks) without modifying the parent `traverse` theme so you can update the parent theme later.

Getting started
---------------
1. Place this folder at `wp-content/themes/traverse-child` alongside the parent theme `traverse`.
2. Activate the child theme from WordPress Admin → Appearance → Themes.

What this child theme provides
------------------------------
- `style.css` — Child theme stylesheet and theme header. Add your CSS rules here to override the parent theme.
- `functions.php` (optional) — Use to enqueue/override scripts and styles or to add small custom PHP tweaks. If present, it should enqueue the child stylesheet after the parent.

Developer notes
---------------
- If the parent theme registers and enqueues its own CSS from `/css/style.css`, the child theme must enqueue its stylesheet to ensure it is loaded afterwards. Example enqueue code in the child `functions.php`:

```php
<?php
function traverse_child_enqueue_styles() {
    wp_enqueue_style( 'traverse-parent-style', get_template_directory_uri() . '/css/style.css' );
    wp_enqueue_style( 'traverse-child-style', get_stylesheet_uri(), array( 'traverse-parent-style' ) );
}
add_action( 'wp_enqueue_scripts', 'traverse_child_enqueue_styles' );
```

- To link templates to the child theme, copy the parent template file into this folder and modify it there.
- Escape output: when adding PHP that prints URLs or titles, use `esc_url()` and `esc_html()`.

Testing
-------
- After activating the child theme, open the frontend and inspect the page head (`<link rel="stylesheet">`) to ensure the child `style.css` is present and loaded after the parent stylesheet.
- Clear caches (browser, WP caching plugins) when changes do not appear.

Support
-------
If you need help customizing the child theme or want me to implement common tweaks (header/footer changes, custom CSS rules, template overrides), tell me what you want changed and I’ll apply it.
