<template lang="">
    <Head>
        <Title>{{ user.firstName + ' ' + user.lastName }}的個人頁</Title>
        <Meta name="description" content="用戶頁面"></Meta>
    </Head>
    <MyHeader></MyHeader>

    <div class="container">
        <div class="row">
            <div v-if="!isLoading" class="col-12 load-text">Loading...</div>
            <div v-else class="col-12">
                <div class="user">
                    <h1 class="user__name">
                        {{ user.firstName + ' ' + user.lastName }}
                    </h1>
                    <img class="user__img" :src="user.image" alt="" />
                    <h2 class="user__title">{{ user.company.title }}</h2>
                    <div class="user__text">
                        <div class="user__age">
                            <span>Age：</span>
                            <span>{{ user.age }}</span>
                        </div>
                        <div class="user__gender">
                            <span>Gender：</span>
                            <span>{{ gender }}</span>
                        </div>
                        <div class="user__email">
                            <span>Email：</span>
                            <span class="ttss">{{ user.email }}</span>
                        </div>
                        <div class="user__phone">
                            <span>Phone：</span>
                            <span>{{ user.phone }}</span>
                        </div>
                        <div class="user__birth">
                            <span>Birth：</span>
                            <span>{{ user.birthDate }}</span>
                        </div>
                        <div class="user__blood">
                            <span>Blood：</span>
                            <span>{{ user.bloodGroup }}</span>
                        </div>
                        <div class="user__height">
                            <span>Hegiht：</span>
                            <span>{{ user.height }} (cm)</span>
                        </div>
                        <div class="user__weight">
                            <span>Weight：</span>
                            <span>{{ user.weight }} (kg)</span>
                        </div>
                        <div class="user__address">
                            <span>Address：</span>
                            <span>{{ user.address.city }}</span>
                        </div>
                    </div>
                </div>
            </div>
            <nuxt-link class="home-link" to="/">首頁</nuxt-link>
        </div>
    </div>
</template>
<script>
import axios from 'axios';

export default {
    data() {
        return {
            user: {},
        };
    },

    computed: {
        isLoading() {
            return Object.keys(this.user).length;
        },
        gender() {
            return this.user.gender === 'male' ? '男' : '女';
        },
    },
    methods: {
        getUserInfo() {
            axios
                .get(`https://dummyjson.com/users/${this.$route.params.id}`)
                .then((res) => {
                    this.user = res.data;
                });
        },
    },
    created() {
        this.getUserInfo();
    },
};
</script>
<style lang="scss">
.load-text {
    font-size: 64px;
    text-align: center;
}

.user {
    text-align: center;
    margin-bottom: 25px;
    &__name {
        margin: 25px 0;
    }
    &__img {
        background-color: #ddd;
        margin-bottom: 5px;
        border-radius: 10px;
    }

    &__title {
        margin: 0;
        font-size: 26px;
    }

    &__text {
        width: 300px;
        margin: 25px auto 0;
    }
}

.home-link {
    text-align: center;
    font-size: 18px;
    text-decoration: none;
    display: inline-block;
    background-color: #333;
    width: 250px;
    padding: 10px 0;
    margin: 0 auto;
    border-radius: 3px;
    box-shadow: 0px 1px 10px rgba($color: #000000, $alpha: 0.15);
    &:link,
    &:visited {
        color: white;
    }
}
</style>
