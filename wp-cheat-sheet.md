


### Get image from folder
```php
<img src="<?php echo get_template_directory_uri(); ?>/assets/img/pics/_DSC3831.jpg" alt="">
```

### Get custom taxonomy's terms
```php
<?php
$terms = get_terms( 'collection_taxonomy', array(
    'orderby'    => 'count',
    'hide_empty' => 0,
) );
foreach ($terms as $term) :
    if ($term->slug == "all"){ //allのslugだけ無視
        continue;
    }
?>
        <a class="collection-item" href="<?php echo get_term_link( $term ); ?>">
            <img src="<?php echo z_taxonomy_image_url($term->term_id); ?>" alt="">
            <div class="item-name"><?php echo $term->name;?></div>
        </a>
<?php
endforeach;
?>
```

### When access to like {url}/information, use home_url
```php
<a class="topics-category" href="<?php echo home_url("information") ?>">すべて</a>
```

### Get category
```php
<?php
$cats = get_categories(
    array(
        'orderby' => 'menu_order',
        'hide_empty' => 0,
    )
);
foreach($cats as $cat) {
?>
        <a class="topics-category" href="<?php echo get_category_link( $cat->term_id ) ?>">
            <?php echo $cat->name; ?>
        </a>
<?php
}
?>
```

### Pagination link ><
```php
<div class="wp-pagination">
<?php

echo paginate_links( array(
    'base' => str_replace( 9999, '%#%', esc_url( get_pagenum_link( 9999 ) ) ),
    'format' => '?paged=%#%',
    'current' => max( 1, get_query_var('paged') ),
    'total' => $the_topics_query->max_num_pages,
    'prev_text' => '<',
    'next_text' => '>',
) );

?>
</div>
```

### Get Default posts
```php
<div class="topics-cards">
        
<?php
$paged = ( get_query_var( 'paged' ) ) ? get_query_var( 'paged' ) : 1;
$the_topics_query = new WP_Query( 
    array(
        "post_type" => "post",
        "paged" => $paged,
));
 
if ( $the_topics_query->have_posts() ) {
    while ( $the_topics_query->have_posts() ) {
        $the_topics_query->the_post();
        get_template_part( 'template-parts/topics-card');
    }
} else {
    echo "投稿が見つかりません";
}

?>

</div>

```
