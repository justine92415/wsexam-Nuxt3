<template lang="">
    <div class="navigation">
        <input type="checkbox" id="nav-toggle" class="navigation__checkbox" />
        <label for="nav-toggle" class="navigation__button">
            <span class="navigation__icon">&nbsp;</span>
        </label>

        <div class="navigation__background">&nbsp;</div>

        <nav class="navigation__nav">
            <ul class="navigation__list">
                <li class="navigation__item">
                    <nuxt-link class="navigation__link" to="/">首頁</nuxt-link>
                </li>
                <li class="navigation__item">
                    <nuxt-link class="navigation__link" :to="`/list`"
                        >串接列表API</nuxt-link
                    >
                </li>
                <li class="navigation__item">
                    <div>色彩模式</div>
                    <MyInput
                        :type="'select'"
                        :value="$colorMode.preference"
                        :optionArr="colorMode"
                        @update="updateColorMode"
                    ></MyInput>
                </li>
            </ul>
        </nav>
    </div>
</template>

<script>
export default {
    data() {
        return {
            colorMode: ['light', 'dark', 'sepia'],
        };
    },
    methods: {
        updateColorMode(payload) {
            this.$colorMode.preference = payload;
        },
    },
};
</script>

<style lang="scss" scoped>
.navigation {
    &__checkbox {
        display: none;
    }
    &__button {
        background-color: white;
        height: 70px;
        width: 70px;
        position: fixed;
        top: 40px;
        right: 40px;
        border-radius: 50%;
        z-index: 2000;
        box-shadow: 0 10px 30px rgba(#333, 0.1);
        text-align: center;
        cursor: pointer;
    }
    &__background {
        height: 60px;
        width: 60px;
        border-radius: 50%;
        position: fixed;
        top: 45px;
        right: 45px;
        background-image: radial-gradient(#fdfdfd, #333);
        z-index: 999;
        transition: transform 0.8s cubic-bezier(0.86, 0, 0.07, 1);
    }
    &__nav {
        height: 100vh;
        position: fixed;
        top: 0;
        right: 0;
        z-index: 1500;

        opacity: 0;
        width: 0;
        transition: all 0.8s;
    }
    &__list {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        list-style: none;
        text-align: center;
        width: 100%;
    }
    &__item {
        margin: 10px;
        & div {
            margin: 50px 0 25px;
            font-size: 30px;
            color: white;
        }
    }
    &__link {
        &:link,
        &:visited {
            display: inline-block;
            font-size: 30px;
            font-weight: 300;
            padding: 10px 20px;
            color: white;
            text-decoration: none;
            text-transform: uppercase;
            background-image: linear-gradient(
                120deg,
                transparent 0%,
                transparent 50%,
                white 50%
            );
            background-size: 250%;
            transition: all 0.4s;

            span {
                margin-right: 15px;
                display: inline-block;
            }
        }

        &:hover,
        &active {
            background-position: 100%;
            color: #333;
            transform: translateX(10px);
        }
    }

    &__checkbox:checked ~ &__background {
        transform: scale(80);
    }

    &__checkbox:checked ~ &__nav {
        opacity: 1;
        width: 100%;
    }

    &__icon {
        position: relative;
        margin-top: 35px;
        &,
        &::before,
        &::after {
            width: 30px;
            height: 2px;
            background-color: #444;
            display: inline-block;
        }

        &::before,
        &::after {
            content: '';
            position: absolute;
            left: 0;
            transition: all 0.2s;
        }

        &::before {
            top: -8px;
        }

        &::after {
            top: 8px;
        }
    }

    &__button:hover &__icon::before {
        top: -10px;
    }

    &__button:hover &__icon::after {
        top: 10px;
    }

    &__checkbox:checked + &__button &__icon {
        background-color: transparent;
    }
    &__checkbox:checked + &__button &__icon::before {
        top: 0;
        transform: rotate(135deg);
    }
    &__checkbox:checked + &__button &__icon::after {
        top: 0;
        transform: rotate(-135deg);
    }
}
</style>
