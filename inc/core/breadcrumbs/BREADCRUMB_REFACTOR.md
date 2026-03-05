# OceanWP Breadcrumb Refactor - Technical Documentation

> [!IMPORTANT]
> **Reference Pull Request:** [https://github.com/oceanwp/oceanwp/pull/553](https://github.com/oceanwp/oceanwp/pull/553)
> **Objective:** Transition the legacy monolithic `inc/breadcrumbs.php` file into a modern, class-based architecture (OOP) to improve maintainability and strictly preserve backward compatibility for over 700,000+ OceanWP users.

---

## 1. Technical Architecture Overview

The system has been modularized and is located in `inc/core/breadcrumbs/`:

*   **`OceanWP_Breadcrumbs_Manager`**: The core **Orchestrator**. It handles page context detection and orchestrates the breadcrumb generation process.
*   **`OceanWP_Breadcrumbs_Compatibility`**: A dedicated integration layer for 3rd-party plugins (Yoast SEO, Rank Math, SEOPress) and WooCommerce global hooks.
*   **`OceanWP_Breadcrumbs_Renderer`**: Processes data into premium HTML with automatic **Schema.org (BreadcrumbList)** microdata support.
*   **`Context Providers`**: Specialized classes (`Singular`, `WooCommerce`, `Simple/Archive`) containing the logic for different page types.

---

## 2. Backward Compatibility & Shim Strategy

*   **Gateway Shim**: `inc/breadcrumbs.php` remains as the entry point, maintaining the legacy `oceanwp_breadcrumb_trail()` function and `OceanWP_Breadcrumb_Trail` class.
*   **Hook Preservation**: All original filters (e.g., `oceanwp_breadcrumb_trail_args`, `oceanwp_breadcrumb_trail_items`) are fully honored.
*   **Child Theme Priority**: Uses `locate_template` in `functions.php` to allow developers to override the system from their Child Theme.

---

## 3. Key Integrated Features

*   **Customizer Integration**: The system automatically retrieves values from `get_theme_mod` for the following settings:
    *   `ocean_breadcrumb_show_title`: Controls the visibility of the last item's title.
    *   `ocean_breadcrumb_separator`: Supports custom separator characters or icons.
    *   `ocean_breadcrumb_home_item`: Displays the Home item as an **Icon**, **Text**, or **Both**.
    *   `ocean_breadcrumb_schema`: Toggle for enabling/disabling SEO Microdata.
*   **Taxonomy Hierarchy**: Full support for displaying deep category hierarchies for **Posts**, **WooCommerce Products**, and **Portfolio** items based on user-defined configurations.
*   **Paged Support**: Automatically adds a link to the post title if the current page is part of a paginated set (e.g., `/page/2/`), improving navigation UX.
*   **HTML & SVG Support**: Enhanced rendering logic that allows for **SVG icons** and **custom HTML** markup within breadcrumb labels, ensuring the design remains premium and flexible.

---

## 4. Meta Information
*   **Committed by**: `PC-0506602` (`viet09cntt@gmail.com`)
*   **Target Repository**: `https://github.com/vietpro123/oceanwp` (Master Branch)
