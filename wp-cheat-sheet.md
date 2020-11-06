```php


// Get image from folder
<img src="<?php echo get_template_directory_uri(); ?>/assets/img/pics/_DSC3831.jpg" alt="">


// Get custom taxonomy's terms
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
