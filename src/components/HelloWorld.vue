<template>
  <div class="hello">
    <ul>
      <li @click="markAsSeen(index)" :class="{'seen':notification.seen}" v-for="(notification, index) in notifications" v-bind:key="index">
        <div class="">
          <span @click="markAsSeen(index)" class="circle"></span>
          <span>
            {{ notification.title }}
          </span>
          <span class="time">
            {{ humanReadable(notification.timestamp) }}
          </span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      notifications: [
        {
          title: "Elon Musk sent you a message",
          seen: false,
          timestamp: 1591106486,
        },
        {
          title: "Mark Zuckerberg sent you a message",
          seen: false,
          timestamp: 1591106376
        },
        {
          title: "Milivoje would like to tag you in a photo",
          seen: false,
          timestamp: 1591106296
        },
        {
          title: "Radivoje liked your comment",
          seen: false,
          timestamp: 1591106196
        },
        {
          title: "BIA wants to know you location",
          seen: false,
          timestamp: 1591106456
        }
      ]
    }
  },
  methods: {
    markAsSeen: function(index) {
      this.notifications[index].seen = true;
    },
    humanReadable: function(ts) {
      var date = new Date(ts * 1000);
      var hours = date.getHours();
      var min = date.getMinutes();
      if(min < 10) {
        min = '0' + min;
      }
      if(hours < 10) {
        hours = '0' + hours;
      }
      return hours + ":" + min;
    },
    sortedItems: function() {
      this.notifications.sort((a, b) => {
        if (a.timestamp > b.timestamp) {
          return -1
        } else if (a.timestamp < b.timestamp) {
          return 1
        } else {
          return 0
        }
      });
    }
  },
  beforeMount() {
    this.sortedItems()
  }
}
</script>


<style scoped>
  ul {
    list-style-type: none;
  }

  li {
    max-width: 500px;
    text-align: left;
    margin: 10px auto;
    background: rgb(66, 218, 210);
    line-height: 50px;
    border-radius: 10px;
    cursor: pointer;
  }

  li.seen {
    background-color: rgb(167, 224, 222);
    transition: .5s;

  }

  li.seen .circle {
    background-color: rgb(241, 174, 143);
    transition: .5s;
  }

  span {
    vertical-align: middle;
  }

  .circle {
    height: 20px;
    width: 20px;
    border-radius: 50%;
    background-color: rgb(255, 81, 0);
    display: inline-block;
    margin: 0 10px;
    cursor: pointer;
  }

  .time {
    float: right;
    margin-right: 10px;
  }
</style>
