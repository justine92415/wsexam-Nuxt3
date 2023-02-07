<template>
    <Head>
        <Title>首頁</Title>
        <Meta name="description" content="首頁"></Meta>
    </Head>
    <MyHeader></MyHeader>
    <main>
        <section class="section-users">
            <div class="container">
                <div class="row">
                    <div class="input-control">
                        <div class="search-box">
                            <MyInput
                                :type="'text'"
                                :value="searchStr"
                                @update="updateSearchStr"
                                :placeholder="'Search name'"
                            ></MyInput>
                        </div>
                        <div class="gender-box">
                            <div class="gender-box__item">
                                <MyInput
                                    :id="'all'"
                                    :type="'radio'"
                                    :group="'gender'"
                                    :radioValue="'all'"
                                    :value="genderRadio"
                                    @update="updateRadioValue"
                                ></MyInput>
                                <label for="all">all</label>
                            </div>
                            <div class="gender-box__item">
                                <MyInput
                                    :id="'male'"
                                    :type="'radio'"
                                    :group="'gender'"
                                    :radioValue="'male'"
                                    :value="genderRadio"
                                    @update="updateRadioValue"
                                ></MyInput>
                                <label for="male">male</label>
                            </div>
                            <div class="gender-box__item">
                                <MyInput
                                    :id="'female'"
                                    :type="'radio'"
                                    :group="'gender'"
                                    :radioValue="'female'"
                                    :value="genderRadio"
                                    @update="updateRadioValue"
                                ></MyInput>
                                <label for="female">female</label>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="container">
                <div class="row">
                    <div class="col-12 load-text" v-if="!isLoading">
                        Loading...
                    </div>
                    <div class="col-3" v-for="user in userList" key="user.id">
                        <MyCard :user="user"></MyCard>
                    </div>
                </div>
            </div>
        </section>
    </main>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            searchStr: '',
            genderRadio: 'all',
            source: [],
        };
    },

    computed: {
        userList() {
            if (this.searchStr !== '') {
                return this.source.filter((user) => {
                    const userFullName = user.firstName + ' ' + user.lastName;
                    if (this.genderRadio === 'all') {
                        return userFullName
                            .toLowerCase()
                            .includes(this.searchStr.toLowerCase());
                    }
                    return (
                        userFullName
                            .toLowerCase()
                            .includes(this.searchStr.toLowerCase()) &&
                        user.gender === this.genderRadio
                    );
                });
            }

            if (this.genderRadio !== 'all') {
                return this.source.filter((user) => {
                    return user.gender === this.genderRadio;
                });
            }

            return this.source;
        },
        isLoading() {
            return this.source.length;
        },
    },

    methods: {
        getAllUser() {
            axios.get('https://dummyjson.com/users').then((res) => {
                let resUsers = res.data.users;
                this.source = resUsers;
            });
        },
        updateSearchStr(payload) {
            this.searchStr = payload;
        },
        updateRadioValue(payload) {
            this.genderRadio = payload;
        },
    },
    created() {
        this.getAllUser();
    },
};
</script>

<style lang="scss">
.input-control {
    display: flex;
    align-items: center;
    margin: 50px auto;

    .search-box {
        margin-right: 20px;
    }

    .gender-box {
        display: flex;

        &__item label {
            display: inline-block;
            margin-left: 5px;
        }

        &__item:not(:last-child) {
            margin-right: 10px;
        }
    }
}

.load-text {
    font-size: 64px;
    text-align: center;
}
</style>
