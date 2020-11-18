
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

// information sidebar
const informationSidebar = document.querySelector<HTMLElement>(
    ".information-sidebar"
);
const footer = document.querySelector<HTMLElement>("footer");
if (document.querySelector(".information-main")) {
    window.addEventListener(
        "scroll",
        () => {
            const isNearFooter =
                footer.offsetTop - (window.scrollY + window.innerHeight) < 100;
            if (isNearFooter) {
                informationSidebar.classList.add("sidebar-hide");
            } else {
                informationSidebar.classList.remove("sidebar-hide");
            }
        },
        { passive: true }
    );
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
 css file
 ```css
 
.information-main {
    display: flex;
    justify-content: flex-end;
    align-items: flex-start;
    width: 100%;
    .information-content {
        margin-right: 10%;
        flex: 0 1 50%;
        display: flex;
        justify-content: flex-start;
        align-items: flex-start;
        flex-direction: column;
        .information-card {
            padding: 4% 0;
            font-family: "Yu Gothic";
            .title {
                font-size: 24px;
                margin-top: 15px;
            }
            .date {
                font-size: 14px;
                color: #555;
                margin: 0px auto 10px 15px;
            }
            .image {
                margin: 15px 0;
                width: 100%;
                height: auto;
            }
            .description {
                font-size: 16px;
                padding: 0 2%;
            }
        }

    }

    .wp-pagination {
        margin: 10% 10% 10% 0;
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        .page-numbers {
            color: #555;
            border-bottom: solid 1px transparent;
            font-size: 18px;
            margin: 0 20px 10px 20px;
            &:hover {
                color: $accent-color;
                border-bottom: solid 1px $accent-color;
            }
        }
        .current {
            color: #ccc;
            &:hover {
                color: #ccc;
                border-bottom: solid 1px transparent;
            }
        }
    }
}

.sidebar-hide {
    opacity: 0 !important;
    visibility: hidden !important;
}

.information-sidebar {
    transition: all .2s;
    visibility: visible;
    opacity: 1;

    position: fixed;
    top: 25%;
    left: 15%;
    width: 25%;
    .sidebar-container {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        font-family: 'Times New Roman',"Yu Mincho", Times, serif;
        font-size: 15px;
        letter-spacing: 1px;
        .title {
            border-bottom: solid 1px #555;
        }
        .information-sidebar-content {
            transition: all .2s;
            margin: 20px 7px;
            color: #000;
            &:hover {
                cursor: pointer;
                color: #888;
            }
        }
    }
}

.sidebar-toggle {
    color: $accent-color !important;
}
```
