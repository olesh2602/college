<template>
  <div class="app-specialities">
    <div class="header">
      <app-title
        :perc="60"
        background="green"
        class="title"
      >Спеціальності</app-title>

      <div class="tips">
        <div class="tip">
          <app-title
            background="green"
            class="block"
          ></app-title>

          <span>3 курси</span>
        </div>

        <div class="tip">
          <app-title
            background="orange"
            class="block"
          ></app-title>

          <span>4 курси</span>
        </div>
      </div>
    </div>

    <div class="list">
      <div
        v-for="(department, index) in departments"
        v-bind:key="index"
        class="column"
        :class="{
          'opened': department.opened,
        }"
      >
        <div
          class="title"
          @click="department.opened = !department.opened"
        >
          <div>{{department.name}}</div>

          <div class="icon">
            <img
              src="@/assets/icons/ChevronTop.svg"
              alt="chevron top"
            />
          </div>
        </div>

        <div
          class="specialities-list"
          v-if="department.specialities"
        >
          <div
            v-for="(speciality, index) in department.specialities"
            v-bind:key="index"
            class="speciality"
            :class="[
              `years-${speciality.years}`,
            ]"
          >
            <div class="icons">
              <div class="icon">
                <img
                  :src="require(`@/assets/icons/specialities/${speciality.code}.svg`)"
                  alt="speciality icon"
                />
              </div>

              <div class="code">{{speciality.code}}</div>
            </div>

            <div class="name">{{speciality.name}}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AppTitle from '@/components/ui/AppTitle.vue'

export default {
  components: {
    AppTitle,
  },
  data() {
    return {
      departments: [
        {
          name: 'Відділення комп\'ютерних технологій',
          opened: false,
          specialities: [
            { code: '121', years: 4, name: 'Інженерія програмного забезпечення' },
            { code: '151', years: 4, name: 'Автоматизація та комп\'ютерно-інтегровані технології' },
          ],
        },
        {
          name: 'Економічне відділення',
          opened: false,
          specialities: [
            { code: '071', years: 3, name: 'Облік і оподаткування' },
            { code: '072', years: 3, name: 'Фінанси, банківська справа та страхування' },
            { code: '073', years: 4, name: 'Менеджмент' },
            { code: '075', years: 3, name: 'Маркетинг' },
          ],
        },
        {
          name: 'Механіко-технологічне відділення',
          opened: false,
          specialities: [
            { code: '133', years: 4, name: 'Галузеве машинобудування' },
            { code: '182', years: 4, name: 'Технологія легкої промисловості' },
            { code: '205', years: 4, name: 'Лісове господарство (спеціалізація: “Деревообробні та меблеві технології”)' },
          ],
        },
      ],
    }
  },
}
</script>

<style lang="less" scoped>
.app-specialities {
  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;

    .title {
      font-size: 22px;
      text-transform: uppercase;
      padding-left: 30px;
    }

    .tips {
      display: flex;
      align-items: center;

      .tip {
        display: flex;
        margin-left: 30px;
        align-items: center;

        .block {
          width: 20px;
          height: 30px;

          margin-right: 5px;
        }
      }
    }
  }

  .list {
    display: grid;
    grid-template-columns: repeat(3, 1fr);

    grid-gap: 45px;

    margin-top: 50px;

    .title {
      font-size: 20px;
      font-weight: 700;
      color: var(--color-font-gray);

      height: 60px;

      .icon {
        display: none;
      }
    }

    .specialities-list {
      margin-top: 20px;

      .speciality {
        padding: 30px;
        margin-bottom: 30px;
        font-size: 16px;

        display: grid;
        grid-template-columns: auto 1fr;
        grid-gap: 20px;

        align-items: center;

        .icons {
          text-align: center;
          font-size: 16px;

          .icon {
            margin-bottom: 5px;
          }
        }

        &.years-4 {
          background: var(--color-accent-orange);
        }

        &.years-3 {
          background: var(--color-accent-green);
        }
      }
    }
  }

  @media screen and (max-width: 1195px) {
    .header {
      flex-direction: column;
      align-items: flex-start;

      .tips {
        margin-top: 40px;

        .tip {
          margin-left: 0;
          margin-right: 30px;
        }
      }
    }

    .list {
      grid-template-columns: 1fr;
      grid-gap: 20px;

      .title {
        display: grid;
        grid-template-columns: 1fr 30px;
        grid-gap: 20px;
        height: auto;

        align-items: center;

        padding: 20px;

        box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.06);

        .icon {
          display: block;
          text-align: center;

          transform: rotate(180deg);
          transition: all .45s;
        }
      }

      .specialities-list {
        display: none;
      }
    }

    .column {
      &.opened {
        .specialities-list {
          display: block;
        }

        .icon {
          transform: rotate(0deg);
        }
      }
    }
  }
}
</style>
