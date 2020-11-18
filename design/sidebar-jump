
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
