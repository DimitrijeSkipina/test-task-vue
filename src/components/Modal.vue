<template>
    <div class="modal-screen">
        <div class="title-box">
            <div class="title-box__left-box">
                <div class="title-box__title-text">Chagenger</div>
                <div class="title-box__description-text">Управление транспортом</div>
            </div>
            <div class="title-box__exit" @click="$emit('closeModal')">
                <img class="title-box__exit-svg" src="/img/shape.svg" alt="exit svg" >
            </div>
        </div>

        <div class="content" ref="contentBlock">
            <div v-for="item in dataArray" :key="item.name" class="content__data-block" @click="handleClick(item)">

                <div class="content__data-block-name">{{ item.name }}</div>

                <div v-if="item.type === 'buying'" class="content__data-block-price">
                    <span class="content__data-block-price--dollar-sign">$</span>{{ item.price }}
                </div>

                <div v-else-if="item.type === 'sale'" class="content__data-block-price">
                    <span class="content__data-block-price--dollar-sign-green">+$</span>{{ item.price }}
                </div>

                <div v-else class="content__data-block-price">
                    <img src="/img/premium.svg" class="content__data-block--premium-img">
                </div>

            </div>
        </div>
    </div>
</template>

<script setup>
import { defineEmits, onMounted } from 'vue';

const closeModal = () => {
  defineEmits(['closeModal']);
  emit('closeModal');
}

const dataArray = [
    { name: "Отправить на стоянку", price: 400, type: "buying" },
    { name: "Назначить семейным", price: 2200, type: "premium" },
    { name: "Отремонтировать", price: 2200, type: "buying" },
    { name: "Продать", price: 99999, type: "sale" },
    { name: "Отправить на стоянку", price: 2200, type: "buying" },
    { name: "Назначить семейным", price: 2200, type: "premium" },
    { name: "Отремонтировать", price: 155, type: "buying" },
    { name: "Отремонтировать", price: 255, type: "buying" },
    { name: "Отремонтировать", price: 99999, type: "buying" },
    { name: "Отремонтировать", price: 455, type: "buying" },
    { name: "Отремонтировать", price: 555, type: "buying" }
];

const handleScroll = (event) => {
    const scrollAmount = event.deltaY;
    contentBlock.scrollLeft += scrollAmount;
};

let contentBlock;

onMounted(() => {
    contentBlock = document.querySelector('.content');
    contentBlock.addEventListener('wheel', handleScroll);

    const items = dataArray.length;

    if (items > 8) {
        contentBlock.classList.add('more-than-eight');
    } else if (items > 4) {
        contentBlock.classList.add('more-than-four');
    } else {
        contentBlock.classList.add('less-than-four');
    }
});


const handleClick = (item) => {
  console.log(item.name);
  const block = event.target.closest('.content__data-block');
  block.classList.add('content__data-block-dark');
};
</script>

<style lang="scss">

.modal-screen {
  width: 100vw;
  height: 100vh;
  background-image: url('/img/SVG-ART.svg'), url('/img/Intersect.png');
  background-repeat: no-repeat;
  background-position: center center;

  .title-box {
    width: 100%;
    height: 20%;
    max-height: 15%;
    padding: 4vw 0;
    padding-left: 9vw;
    padding-right: 2vw;
    display: flex;
    align-items: center;
    flex-direction: row;
    justify-content: space-between;

    .title-box__left-box {
      height: 100%;
      max-height: 100%;
      display: flex;
      flex-direction: row;
      align-items: center;

      .title-box__title-text {
        font-size: 4vw;
        font-weight: 500;
        color: white;
        text-transform: uppercase;
      }

      .title-box__description-text {
        font-size: 2.2vw;
        color: #f1f1f180;
        padding-left: 3vw;
      }
    }

    .title-box__exit {
      text-align: center;
      display: flex;
      align-items: center;
      justify-content: center;
      width: 5vw;
      height: 5vw;
      border-radius: 50%;
      cursor: pointer;
      background-image: linear-gradient(transparent, #f1f1f129); 

      &:hover {
        background-image: linear-gradient(transparent, #f1f1f144);
      }

      .title-box__exit-svg {
        width: 35%;
        height: 35%;
      }
    }
  }

  .content {
    width: 100%;
    height: 85%;

    &.more-than-eight {
      display: flex;
      flex-direction: column;
      overflow-y: scroll;
      padding: 0 9vw;
      padding-top: 2vw;
      flex-wrap: wrap;
      align-content: flex-start;
      justify-content: flex-start;

      -ms-overflow-style: none;
      &::-webkit-scrollbar { 
        width: 0;
      }
    }

    &.more-than-four {
      max-width: 100%;
      display: flex;
      padding: 0 9vw;
      flex-wrap: wrap;
      align-content: center;
      justify-content: flex-start;
    }

    &.less-than-four {
      display: flex;
      padding: 0 9vw;
      align-items: center;
      justify-content: center;
    }

    .content__data-block {
      min-width: 18vw;
      max-width: 18vw;
      margin: 1vw;
      height: 30vh;
      border-radius: 1vh;
      background: linear-gradient(#141A1E, #141a1e6a); 
      padding: 2%;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      cursor: pointer;
      transition: background-color 0.2s ease;

      &.content__data-block-dark {
        background-color: rgba(20, 26, 30, 0.8);
      }

      .content__data-block-name {
        font-size: 1.7vw;
        color: white;
        font-weight: 500;
      }

      .content__data-block-price {
        color: white;
        font-size: 2vw;
        display: flex;
        font-weight: 600;

        &--dollar-sign {
          color: #ffbb00;
          font-weight: 600;
          padding-right: 0.5vw;
        }

        &--dollar-sign-green {
          color: #11ff00;
          font-weight: 600;
          padding-right: 0.5vw;
        }
      }

      .content__data-block--premium-img {
        width: 2.5vw;
        object-fit: contain;
        opacity: 0.4;
      }
    }
  }
}
</style>

