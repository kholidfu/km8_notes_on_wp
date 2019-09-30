# WORDPRESS TIPS & TRICKS

## Template

## Important to read
URL untuk gallery index --> /km/ templatenya ada di `page.php`
untuk sub-page nya -> `gallery-sitemap-page.php`

ke depan mungkin perlu dirapiken...

### Turn on debug
go to `wp-config.php` change 

`define( 'WP_DEBUG', false );`

to

`define( 'WP_DEBUG', true );`

### How to Use this template
- setting wordpress di hosting
- setting permalink ke `Post name`
- 

### Create custom thumbnail size (hard crop)
1. Tambahkan baris berikut di `functions.php`
    ```
    <?php
        // 260 pixels wide by 180 pixels tall, hard crop mode
        add_image_size( 'custom-size', 260, 180, true );
    ?>
    ```

2. Panggil di template menggunakan fungsi berikut:
```
   <?php echo wp_get_attachment_image($attachment->ID, 'custom-size', false, array('alt' => 'asdasdas', 'title' => 'asdasdsa')); ?>
```

### Calling wp built-in func from outside world
imagine you have custom-file.php in your template directory... How to use WP built-in func? Simple
```
<?php
    require_once("../../../wp-load.php");

    echo get_site_url();
?>
```

### Show admin bar
```
<?php wp_footer(); ?>
```

## Query

### Get Post ID on single post / attachment
```
<?php
    $post_id = get_queried_object_id();
?>
```


### Check query available on current page
```

<?php
    echo '<pre dir="ltr">';
    print_r($GLOBALS['wp_query']);
    echo '</pre>';
?>
```

Untuk membuat custom query, cukup buat variable baru dengan argumen sesuai dengan yang diinginkan...

Misal kita ingin mengurutkan post `"DESC"` dan membatasi `posts_per_page = 5`:

```
<?php
    $the_query = new WP_Query([
        'order'             =>'DESC',
        'posts_per_page'    => 5,
    ]);
?>
```

Jika kita `print_r($the_query)`, maka kita akan dapatkan query yang kita inginkan...

### index.php

```
<?php
    // prepare the query, order by ASC (chronological order)
    $the_query = new WP_Query([
        'order'=>'DESC',
    ]);
?>
<?php 
    // loop through all post
    if ( $the_query->have_posts() ) : while ( $the_query->have_posts() ) : $the_query->the_post(); 

        // $the_query->post   // <== post object
        echo $the_query->post->post_title;

    endwhile;
    endif;
?>
```

## Others

### Display all errors when developing PHP template
```
<?php
    ini_set('display_errors', 1);
    ini_set('display_startup_errors', 1);
    error_reporting(E_ALL);
?>
```

## References
- https://www.binarymoon.co.uk/2010/03/5-wordpress-queryposts-tips/
- 
