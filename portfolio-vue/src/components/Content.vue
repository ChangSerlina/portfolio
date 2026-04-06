<template>
    <div class="flex container">
        <div class="col-6 col-lg-12" id="intro">
            <h3>Hi, I am</h3>
            <h2 id="name">Serlina</h2>
            <p>A backend engineer mainly working with PHP and Laravel. I have experience with Linux, Docker, Nginx, Apache, and MySQL, and I'm familiar with GitLab CI/CD and SonarQube for automation and code quality management.</p>
            <button type="button" class="consultation-btn" @click="showForm = true">schedule free consultation</button>
            or <span class="highlight">Email me at <a href="mailto:serlina0818@yahoo.com.tw">serlina0818@yahoo.com.tw</a></span>
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
    
    <!-- 諮詢表單模態框 -->
    <ConsultationForm :isOpen="showForm" @close="showForm = false" />
</template>

<script setup>
import { ref } from 'vue'
import ConsultationForm from './ConsultationForm.vue'

const showForm = ref(false)
</script>

<style>
.container {
    padding-top: 6rem;
    position: absolute;
    align-items: center;
    @media (min-width: 768px) {
        height: 85vh;
    }
}

.container p {
    text-align: justify;
}

#name {
    margin-top: -16px;
}

#intro {
    margin-bottom: 4rem;
}

.consultation-btn {
    padding: 0.75rem 1.5rem;
    font-size: 1rem;
    background-color: #4a90e2;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-weight: 500;
    transition: background-color 0.2s, transform 0.1s;
}

.consultation-btn:hover {
    background-color: #357abd;
    transform: translateY(-2px);
}

.consultation-btn:active {
    transform: translateY(0);
}

#skill {
    display: flex;
    flex-direction: column;
    align-items: center;
    @media (max-width: 1024px) {
        margin-bottom: 1rem;
    }
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

.highlight {
  text-decoration: none;
  background-image: linear-gradient(#ffeb3b, #ffeb3b);
  background-repeat: no-repeat;
  background-size: 100% 25%;
  background-position: 0 100%;
}
/* 中螢幕 */
@media (max-width: 1024px) {
    .container {
        width: 90%;
        padding-top: 3rem;
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
/* 小螢幕 */
@media (max-width: 425px) {
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