# News Portal - PHP Web Application

## Overview
This is a PHP-based News Portal web application that allows users to browse, search, and read news articles. The application features a clean Bootstrap-based responsive design and includes functionality for displaying news posts, categories, search capabilities, and user comments.

## What's Happening in This Repository

### 📂 File Structure & Functionality

#### **Core Pages:**

1. **`index.php`** - Homepage
   - Displays paginated list of news articles (8 per page)
   - Shows article previews with images, titles, categories, and posting dates
   - Implements pagination with First/Previous/Next/Last navigation
   - Links to detailed article views and category pages

2. **`news-details.php`** - Article Detail Page
   - Shows full article content with images
   - Implements CSRF-protected comment system
   - Displays approved user comments with timestamps
   - Handles comment submission with admin moderation

3. **`category.php`** - Category-specific News
   - Filters and displays news articles by category
   - Uses session storage for category persistence
   - Implements same pagination system as homepage
   - Shows category-specific article listings

4. **`search.php`** - Search Functionality
   - Allows users to search news articles by title
   - Uses LIKE queries for text matching
   - Displays search results in card format
   - Includes pagination for search results

5. **`about-us.php`** - About Page
   - Dynamic content loaded from database (`tblpages` table)
   - Displays page title and description from DB

6. **`contact-us.php`** - Contact Page
   - Similar to about page, loads content from database
   - Shows contact information dynamically

### 🗄️ Database Integration

The application connects to a MySQL database with the following key tables:

- **`tblposts`** - Stores news articles
  - Fields: id, PostTitle, PostImage, PostDetails, PostingDate, CategoryId, SubCategoryId, Is_Active
  
- **`tblcategory`** - News categories
  - Fields: id, CategoryName
  
- **`tblsubcategory`** - News subcategories
  - Fields: SubCategoryId, Subcategory
  
- **`tblcomments`** - User comments
  - Fields: postId, name, email, comment, status, postingDate
  
- **`tblpages`** - Static page content
  - Fields: PageName, PageTitle, Description

### 🔧 Key Features

#### **Pagination System:**
- Displays 8 articles per page
- Calculates total pages based on record count
- Provides First/Previous/Next/Last navigation
- Consistent across all listing pages

#### **Security Measures:**
- CSRF token protection for comment forms
- Input sanitization with `htmlentities()`
- SQL injection prevention with `intval()` for IDs
- Session-based token generation and verification

#### **Comment System:**
- Users can submit comments with name, email, and message
- Comments require admin approval (status = 0 initially)
- Only approved comments (status = 1) are displayed
- CSRF protection prevents unauthorized submissions

#### **Search Functionality:**
- Text-based search in article titles
- Case-insensitive matching with LIKE queries
- Results displayed in same card format as other pages

### 🎨 Frontend Design

#### **Bootstrap Integration:**
- Uses Bootstrap 4 for responsive design
- Custom CSS file: `css/modern-business.css`
- jQuery and Bootstrap JavaScript libraries
- Card-based layout for articles

#### **Responsive Layout:**
- Main content area (col-md-8)
- Sidebar area (included via `includes/sidebar.php`)
- Navigation header (`includes/header.php`)
- Footer (`includes/footer.php`)

### 📁 Missing Dependencies

The application references several files/directories that are not present in the repository:

#### **Include Files:**
- `includes/config.php` - Database configuration
- `includes/header.php` - Navigation menu
- `includes/sidebar.php` - Sidebar widgets
- `includes/footer.php` - Footer content

#### **Asset Directories:**
- `vendor/bootstrap/css/bootstrap.min.css`
- `vendor/jquery/jquery.min.js`
- `vendor/bootstrap/js/bootstrap.bundle.min.js`
- `css/modern-business.css`
- `admin/postimages/` - Directory for article images

### 🔍 Code Analysis

#### **Strengths:**
1. **CSRF Protection** - Proper token implementation in comment forms
2. **Input Sanitization** - Uses `htmlentities()` for output escaping
3. **Pagination** - Well-implemented pagination system
4. **Responsive Design** - Bootstrap-based mobile-friendly layout
5. **Modular Structure** - Separate includes for header, footer, sidebar

#### **Areas for Improvement:**
1. **SQL Injection** - Direct variable interpolation in SQL queries
2. **Error Handling** - Limited error checking and user feedback
3. **Code Organization** - Mixed PHP and HTML could be better separated
4. **Input Validation** - Missing server-side validation for forms
5. **Session Security** - No session timeout or regeneration

### 🚀 How It Works

1. **Homepage Flow:**
   ```
   User visits index.php → 
   Database queries for active posts → 
   Displays paginated article list → 
   User clicks "Read More" → 
   Redirects to news-details.php with article ID
   ```

2. **Comment System Flow:**
   ```
   User fills comment form → 
   CSRF token verified → 
   Comment saved with status=0 → 
   Admin reviews and approves → 
   Comment appears on article page
   ```

3. **Search Flow:**
   ```
   User enters search term → 
   search.php queries database → 
   Results displayed with pagination → 
   User can click through to full articles
   ```

### 🎯 Purpose & Use Cases

This News Portal application is designed for:
- **News Websites** - Publishing and managing news articles
- **Blogs** - Content management with categories
- **Community Sites** - User engagement through comments
- **Educational Projects** - Learning PHP/MySQL development

The application provides a solid foundation for a content management system with modern web standards and security considerations.