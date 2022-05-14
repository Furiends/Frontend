<template>
  <view class="content">
    <view class="uni-form-item uni-column">
      <input
        class="uni-input"
        v-model="inputValue"
        @input="onKeyInput"
        placeholder="请输入"
      />
    </view>
    <view
      class="list-container"
      v-for="country in contries"
      :key="country.name"
    >
      <image class="imag" :src="country.src"></image>
      <view class="detial">
        <view class="name">{{ country.name }}</view>
        <view
          >Populations: <text>{{ country.populations }}</text></view
        >
        <view
          >Region: <text>{{ country.region }}</text></view
        >
        <view
          >Capital: <text>{{ country.capital }}</text></view
        >
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      inputValue: '',
      contries: [],
      timeout: null,
    };
  },
  onLoad() {
    this.contries = this.loadAll();
  },
  methods: {
    querySearchAsync(event, cb) {
      var contries = this.contries;
      var results = event.target.value
        ? contries.filter(this.createStateFilter(event.target.value))
        : contries;

      clearTimeout(this.timeout);
      this.timeout = setTimeout(() => {
        cb(results);
      }, 3000 * Math.random());
    },
    createStateFilter(queryString) {
      return (inputValue) => {
        return (
          inputValue.name.toLowerCase().indexOf(queryString.toLowerCase()) === 0
        );
      };
    },
    onKeyInput: function (event) {
      const cs = this.loadAll();
      if (this.inputValue) {
        const res = cs.filter(
          (item) => item.name.toLowerCase() === event.target.value
        );
        this.contries = res;
      } else {
        this.contries = cs;
      }
    },
    loadAll: function () {
      return [
        {
          name: 'Germany',
          src: 'https://upload.wikimedia.org/wikipedia/en/thumb/b/ba/Flag_of_Germany.svg/1600px-Flag_of_Germany.svg.png?20111003033442',
          populations: 81770990,
          region: 'Europe',
          capital: 'Berlin',
        },
        {
          name: 'Iceland',
          src: 'https://upload.wikimedia.org/wikipedia/en/thumb/b/ba/Flag_of_Germany.svg/1600px-Flag_of_Germany.svg.png?20111003033442',
          populations: 81770990,
          region: 'Europe',
          capital: 'Berlin',
        },
      ];
    },
  },
};
</script>

<style>
.content {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  color: #fff;
  font-family: 'Nunito Sans';
}

.list-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 20rem;
  width: 15rem;
  border-radius: 20rem;
  margin-top: 2rem;
}

.list-container > view {
  flex: 1;
}

.imag {
  width: 100%;
  height: 50%;
  border-top-left-radius: 1em;
  border-top-right-radius: 1em;
}

.detial {
  box-sizing: border-box;
  padding: 2rem;
  background-color: #424951;
  width: 100%;
  border-bottom-left-radius: 1em;
  border-bottom-right-radius: 1em;
}

.detial .name {
  margin-bottom: 1rem;
  font-weight: bold;
}

.detial text {
  margin-left: 0.5rem;
  margin-top: 1rem;
}

input {
  height: 28px;
  line-height: 28px;
  font-size: 15px;
  padding: 0px;
  flex: 1;
  background-color: #ffffff;
  color: red;
}
</style>
