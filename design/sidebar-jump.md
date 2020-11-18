
### Jump to the fixed sidebar tag.
```ts
//scroll to hash in information page
const sidebarContents = document.querySelectorAll<HTMLElement>(
    ".information-sidebar-content"
);
const infoCards = document.querySelectorAll<HTMLElement>(".information-card");
if (isExist(sidebarContents)) {
    sidebarContents.forEach((el) => {
        el.addEventListener("click", () => {
            scrollToTag(el.dataset.tag);
        });
    });
    window.addEventListener(
        "scroll",
        () => {
            infoCards.forEach((el) => {
                let targetMenu;
                sidebarContents.forEach((sideEl) => {
                    if (sideEl.dataset.tag == el.dataset.tag) {
                        targetMenu = sideEl;
                    }
                });
                const switchPos =
                    window.pageYOffset > el.offsetTop - 200 &&
                    window.pageYOffset <= el.offsetTop + el.offsetHeight - 200;
                toggleClassList(targetMenu, switchPos, "sidebar-toggle");
                // if (switchPos) {
                //     targetMenu.style.color = "red";
                // } else {
                //     targetMenu.style.color = "black";
                // }
            });
        },
        { passive: true }
    );
}
function scrollToTag(tag) {
    infoCards.forEach((el) => {
        if (el.dataset.tag == tag) {
            const tagPos = el.offsetTop - 100;
            window.scrollTo(0, tagPos);
        }
    });
}
```

php file
```php
<?php
get_header();
$title_array = [];
$jumpIndex = 0;
?>
<div class="information-main">

    <!-- content -->
    <section class="information-content">

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

        array_push($title_array, get_the_title());

?>
        <div data-tag="<?php echo $jumpIndex; ?>" class="information-card">
            <div class="title"><?php the_title(); ?></div>
            <div class="date"><?php echo get_the_date(); ?></div>
            <?php if (get_the_post_thumbnail()): ?>
            <div class="image">
                <img src="<?php echo the_post_thumbnail_url(); ?>" alt="">
            </div>
            <?php endif; ?> 
            <div class="description"><?php the_content(); ?></div>
        </div>
<?php
        $jumpIndex ++;
    }
} else {
    echo "投稿が見つかりません";
}

?>

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

    </section>
    <!-- sidebar -->
    <section class="information-sidebar">
        <div class="sidebar-container">
            <div class="title">INFORMATION</div>
<?php
foreach($title_array as $key=>$title):
?>
            <div class="information-sidebar-content" data-tag="<?php echo $key;?>">
                <?php echo $title; ?>
            </div>

<?php
endforeach;
?>
        </div>

    </section>



</div>
<?php
get_footer();
?>
 ```
