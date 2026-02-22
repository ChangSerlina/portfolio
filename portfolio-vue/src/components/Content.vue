<template>
    <div class="flex container">
        <div class="col-6 col-lg-12">
            <h3>Hi, I am</h3>
            <h2 id="name">Serlina</h2>
            <p>A backend engineer mainly working with PHP and Laravel. I have experience with Linux, Docker, Nginx, Apache, and MySQL, and I'm familiar with GitLab CI/CD and SonarQube for automation and code quality management.</p>
            <a href="http://" target="_blank" rel="noopener noreferrer"><input type="button" value="schedule free consultation" /></a>
        </div>
        <div class="col-5 col-lg-12" id="skill">
            <div class="flex" id="skills">
                <p>Web Design</p>
                <p>LNMP</p>
                <p>Docker</p>
            </div>
            <div class="img" id="img2"></div>
        </div>
    </div>
</template>

<script setup></script>

<style>
.container {
    padding-top: 6rem;
    position: absolute;
    align-items: center;
}

.container p {
    text-align: justify;
}

#name {
    margin-top: -16px;
}

#skill {
    display: flex;
    flex-direction: column;
    align-items: center;
}

#skills {
    width: 100%;
    height: 120px;
}

#skills p {
    background-image: url('https://img.icons8.com/?size=160&id=11871&format=png&color=000000');
    background-repeat: no-repeat;
    background-position: center;
    text-align: center;
    height: 7rem;
    width: 15rem;
    display: flex;
    align-items: center;
    /* 垂直置中 */
    justify-content: center;
    /* 水平置中 */
}

#skills p:nth-child(odd) {
    position: relative;
    top: 24px;
}

#skills p:nth-child(even) {
    position: relative;
    top: -55px;
}

#img2 {
    height: 20rem;
    width: 25.5rem;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    background-image: url('@/assets/images/點點.jpg');
    border-radius: 173px;
}

/* 中螢幕 */
@media (max-width: 1024px) {
    .container {
        width: 80%;
        padding-top: 0.5rem;
        flex-flow: column;
    }

    #img2 {
        height: 13rem;
        width: 17rem;
        border-radius: 130px;
    }

    #skills p {
        background-image: url('https://img.icons8.com/?size=120&id=11871&format=png&color=000000');
    }
}
</style>