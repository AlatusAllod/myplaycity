<template>
  <div :class="$style.card">
    <aside :class="[$style.info, {[$style['info--open']]: data.isOpen}]">
      <header :class="$style.id">
        <div>{{ data.id }}</div>
        <img :class="$style.icon" src="../assets/img/checkmark.png" alt="checkmark">
      </header>
      <footer :class="$style.hoursCounter">{{ data.isOpen ? countOpenHours() + 'h' : 'Closed' }}</footer>
    </aside>
    <main :class="$style.main">
      <h4 :class="$style.title">{{ data.issue }}</h4>
      <span :class="$style.timestamp">Guest {{makeDate()}}</span>
    </main>
    <button :class="$style.button"></button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      monthNames: [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December"
      ]
    };
  },
  props: {
    data: Object
  },
  methods: {
    countOpenHours() {
      return Math.floor(
        (Date.parse(new Date()) - Date.parse(this.data.openDate)) /
          1000 /
          60 /
          60
      );
    },
    makeDate() {
      const date = this.data.openDate;
      const hours = date.getHours();
      let minutes = date.getMinutes();
      if (minutes < 10) {
        minutes = "0" + minutes;
      }
      let result = `${hours}:${minutes}`;
      if (this.countOpenHours() > 24) {
        result += ` - ${date.getDate()} ${this.monthNames[date.getMonth()]}`;
      }
      return result;
    }
  }
};
</script>

<style lang="sass" module>
  .card
    /* Display & Box Model */
    display: flex
    padding: 20px
    margin-bottom: 20px
    background-color: rgb(255,255,255)
    border-radius: 6px

    /* Positioning */
    position: relative
  .info
    /* Display & Box Model */
    display: flex
    flex-direction: column
    justify-content: space-between
    align-items: flex-start
    height: 100px
    margin-right: 20px
    background-color: rgb(243,243,243)
    border-radius: 4px
    &--open
      .id
        /* Display & Box Model */
        height: auto
        background-color: rgb(0, 189, 238)

        /* Positioning */
        position: relative
        &::after
          /* Display & Box Model */
          content: ''
          border: 5px solid transparent
          border-top: 5px solid rgb(0, 189, 238)

          /* Positioning */
          position: absolute
          bottom: -10px
          left: 10px
      .hoursCounter
        /* Display & Box Model */
        border-radius: 0
        background-color: transparent

        /* Text */
        color: rgb(173, 173, 173)
      .icon
        /* Display & Box Model */
        display: none
  .id
    /* Display & Box Model */
    display: flex
    flex-direction: column
    align-items: center
    height: 100%
    padding: 5px
    background-color: rgb(82, 189, 123)
    border-radius: 4px

    /* Text */
    color: white
    font-weight: bold
  .hoursCounter
    /* Display & Box Model */
    padding: 5px
    width: 100%
    background-color: rgb(82, 189, 123)
    border-radius: 4px

    /* Text */
    font-size: .9rem
    font-weight: bold
    color: white
    text-align: center
  .icon
    /* Display & Box Model */
    height: calc(100% - 18px)
    transform: scale(.6)
  .main
    /* Display & Box Model */
    display: flex
    flex-direction: column
    justify-content: space-between
    width: 100%
  .title
    /* Display & Box Model */
    margin: 0
    opacity: .7

    /* Text */
    font-weight: normal
  .timestamp
    /* Display & Box Model */
    padding: 5px
    opacity: .3

    /* Text */
    font-size: .9rem
  .button
    /* Display & Box Model */
    width: 30px
    height: 30px
    padding: 0
    border: 1px solid lightgrey
    border-radius: 50%
    background-color: transparent

    /* Positioning */
    position: absolute
    bottom: 20px
    right: 20px

    /* Other */
    cursor: pointer
    transition: transform .5s
    &:hover,
    &:focus
      /* Display & Box Model */
      transform: rotate(180deg) scale(1.1)
    &::after,
    &::before
      /* Display & Box Model */
      content: ''
      height: 50%
      width: 2px
      background-color: lightgrey
      border-radius: 5px
      transform: translate(-50%, -50%)

      /* Positioning */
      position: absolute
      top: 50%
      left: 50%
    &::before
      /* Display & Box Model */
      transform: translate(-50%, -50%) rotate(90deg)
</style>
