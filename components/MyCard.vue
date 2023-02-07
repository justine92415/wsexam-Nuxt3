<template>
    <div class="card">
        <div class="card-head">
            <div class="card-head__img-box">
                <img class="card-head__img" :src="user.image" />
            </div>
            <div class="card-head__text">
                <h2 class="card-head__text--name">
                    {{ user.firstName + ' ' + user.lastName }}
                </h2>
                <div class="card-head__text--address">
                    {{ user.address.city }}
                </div>
                <div class="card-head__text--birthday">
                    {{ user.birthDate }}
                </div>
            </div>
        </div>
        <div class="card-body">
            <div class="card-body__desc">
                Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quis
                minima corporis molestiae, officia nam rerum.
            </div>
            <div class="card-body__info">
                <div class="card-body__sex">{{ user.gender }}</div>
                <div class="card-body__age">Age:{{ user.age }}</div>
                <div class="card-body__height">H:{{ user.height }}</div>
                <div class="card-body__weight">W:{{ user.weight }}</div>
            </div>
        </div>

        <div class="card-footer">
            <nuxt-link :to="`/user/${user.id}`" class="card-footer__detail"
                >Details</nuxt-link
            >
        </div>
    </div>
</template>
<script>
export default {
    props: ['user'],
};
</script>
<style lang="scss" scoped>
.card {
    width: 275px;
    margin: 0 auto;
    padding: 30px 20px;
    background-color: #fff;
    border-radius: 3px;
    margin-bottom: 30px;
    box-shadow: 0px 1px 10px rgba($color: #000000, $alpha: 0.15);
    transition: all 0.3s;
    &:hover {
        transform: translateY(-10px);
        box-shadow: 0px 1px 20px rgba($color: #000000, $alpha: 0.3);
    }
    &-head {
        display: flex;
        align-items: center;
        margin-bottom: 30px;

        &__img-box {
            position: relative;
            &::after {
                content: '';
                width: 80px;
                height: 80px;
                border-radius: 50%;
                border: 1px solid black;
                background-color: #fa0;
                position: absolute;
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%);
            }
        }

        &__img {
            width: 75px;
            height: 75px;
            border-radius: 50%;
            position: relative;
            z-index: 1;
        }

        &__text {
            width: 100%;
            text-align: center;

            &--name {
                margin: 0 0 10px 0;
                font-size: 18px;
            }
            &--address {
                font-size: 16px;
                margin-bottom: 10px;
            }
        }
    }
    &-body {
        margin-bottom: 30px;
        &__desc {
            font-size: 20px;
            margin-bottom: 20px;
            text-align: justify;
            word-break: break-all;
        }
        &__info {
            display: flex;
            justify-content: space-between;
        }
    }
    &-footer {
        text-align: center;
        &__detail {
            text-decoration: none;
            display: inline-block;
            background-color: #fa0;
            width: 100%;
            padding: 10px 0;
            border-radius: 3px;
            box-shadow: 0px 1px 10px rgba($color: #000000, $alpha: 0.15);
            &:link,
            &:visited {
                color: white;
            }
        }
    }
}
</style>
