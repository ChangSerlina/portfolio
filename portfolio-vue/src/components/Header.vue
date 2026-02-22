<template>
    <div class="flex nav">
        <!-- 左邊LOGO -->
        <div class="col-2 logo">Serlina</div>

        <!-- 大螢幕選單 -->
        <div class="col-8 menu" v-if="!isMobile">
            <ul class="tabs">
                <li v-for="tab in tabs" :key="tab" :class="{ active: activeTab === tab }" @click="activeTab = tab">
                    {{ tab }}
                </li>
            </ul>
        </div>

        <!-- 右邊icon -->
        <div class="col-2 icon" v-if="!isMobile">
            <img src="https://img.icons8.com/?size=25&id=132&format=png&color=000000" alt="搜尋" />
            <img src="https://img.icons8.com/?size=25&id=22396&format=png&color=000000" alt="使用者" />
        </div>

        <!-- 小螢幕漢堡icon -->
        <div class="col-2 menu-mobile" v-if="isMobile">
            <img src="https://img.icons8.com/?size=50&id=78290&format=png&color=000000" alt="menu" class="menu-icon"
                @click="toggleMenu" />
            <!-- 下拉選單 -->
            <ul v-if="showMenu" class="dropdown">
                <li v-for="tab in tabs" :key="tab" :class="{ active: activeTab === tab }" @click="activeTab = tab">
                    {{ tab }}
                </li>
                <img src="https://img.icons8.com/?size=25&id=132&format=png&color=000000" alt="搜尋" />
                <img src="https://img.icons8.com/?size=25&id=22396&format=png&color=000000" alt="使用者" />
            </ul>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

const isMobile = ref(window.innerWidth < 768);
const showMenu = ref(false);

// 頁籤列表
const tabs = ["Home", "About Me", "Projects", "Contact Me"]

// 當前 active 的頁籤，預設 Home
const activeTab = ref("Home")

const checkScreen = () => {
    isMobile.value = window.innerWidth < 768;
    if (!isMobile.value) showMenu.value = false; // 回到大螢幕自動關閉選單
};

const toggleMenu = () => {
    showMenu.value = !showMenu.value;
};

onMounted(() => {
    window.addEventListener("resize", checkScreen);
});

onBeforeUnmount(() => {
    window.removeEventListener("resize", checkScreen);
});
</script>

<style>
.flex {
    display: flex;
}

.nav {
    justify-content: space-between;
    align-items: center;
}

.tabs {
    display: flex;
    justify-content: space-around;
    gap: 20px;
    list-style: none;
    padding: 0;
    margin: 0;
}

.tabs li {
    cursor: pointer;
}

.tabs li.active {
    border-bottom: #007bff 2px solid;
}

.icon {
    display: flex;
    justify-content: flex-end;
}

.icon img {
    padding: 0 10px;
    cursor: pointer;
}

/* 小螢幕隱藏大選單 */
@media (max-width: 768px) {
    .menu {
        display: none;
    }

    .menu-icon {
        cursor: pointer;
        width: 30px;
        height: 30px;
    }

    .dropdown {
        z-index: 2;
        text-align: center;
        /* 讓裡面文字與圖片都置中 */
        position: absolute;
        top: 68px;
        /* header 高度 */
        left: 0;
        right: 0;
        background: white;
        list-style: none;
        margin: 0;
        padding: 10px 0;
        box-shadow: inset 0 -4px 0;
    }

    .dropdown li {
        padding: 10px;
        text-align: center;
    }

    .dropdown li.active {
        background-color: #B6DBF2;
    }

    .dropdown img {
        padding: 10px;
        cursor: pointer;
    }
}
</style>
