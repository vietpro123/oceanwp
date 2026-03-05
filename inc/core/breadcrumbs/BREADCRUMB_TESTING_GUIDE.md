# OceanWP Breadcrumb Refactor - Testing Guide

This guide outlines the steps required to verify the stability and correctness of the new class-based breadcrumb system.

---

## 1. Customizer & UI Testing
1.  **Home Item Configuration**: 
    *   Navigate to *Customizer > General Options > Breadcrumbs*.
    *   Switch "Home Item" between **Icon**, **Text**, and **Both**.
    *   Verify the Home breadcrumb updates instantly in the preview.
2.  **Separator Customization**:
    *   Change the "Breadcrumb Separator" character or icon.
    *   Verify the change reflects correctly between list items.
3.  **Title Visibility**:
    *   Toggle "Show Title" on/off.
    *   Verify the last item in the trail (current page title) appears or disappears.
4.  **Schema.org Validation**: 
    *   Open any page on the frontend.
    *   Copy the URL/HTML and run it through the [Google Rich Results Test](https://search.google.com/test/rich-results).
    *   Ensure the `BreadcrumbList` is detected without errors.

---

## 2. Context & Logic Testing
1.  **Singular Posts & Hierarchy**: 
    *   Create a post with a nested category structure (`Parent > Child`).
    *   In Customizer, set "Posts Taxonomy" to "Category".
    *   Verify the trail: `Home > Parent > Child > Post Title`.
2.  **WooCommerce Integration**: 
    *   Visit the main **Shop** page.
    *   Visit a **Product Category** page.
    *   Visit a **Single Product** page.
    *   Verify the path follows the WooCommerce shop base and category hierarchy.
3.  **Special Pages**:
    *   **Search**: Perform a search and verify the "Search results for..." label.
    *   **404**: Visit a non-existent URL and verify the "404 Not Found" label.
    *   **Archives**: Test Author, Date, and Tag archives.

---

## 3. 3rd-Party Plugin Compatibility
1.  **SEO Plugin Priority**:
    *   Install **Yoast SEO** or **Rank Math**.
    *   Activate their breadcrumb feature.
    *   In *Customizer > Breadcrumbs*, select the plugin as the **Breadcrumb Source**.
    *   Verify that the plugin's breadcrumbs are rendered within the theme's styled container.

---

## 4. Developer Verification
1.  **Child Theme Support**: 
    *   Copy `oceanwp/inc/breadcrumbs.php` to your Child Theme.
    *   Make a small change (e.g., add a comment).
    *   Verify that the theme loads the Child Theme version (Developer Tool > Network/Check file source).
2.  **PHP Compatibility**: 
    *   Ensure no Fatal Errors or Warnings are thrown in PHP 7.4 through PHP 8.3+.
