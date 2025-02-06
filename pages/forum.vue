<template>
    <div class="container mt-5">
      <div class="row justify-content-center">
        <TableList />
      </div>
      <div class="comment mt-2">
        <TableComment :tableData="tableData" />
      </div>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent } from 'vue';
  export default defineComponent({
  
    setup() {
      const tableData = [
        {
          topic: '熱門討論區 😺😺',
          link: '/forumdetail?id=nba1',
          image: 'https://picsum.photos/100/100',
          imagelink: '#',
          author: {
            name: '張志明',
            link: '#',
            date: '03-20 19:15'
          },
          latestReply: {
            author: '李家豪',
            link: '#',
            date: '04-11 20:59'
          }
        },
  
        {
          topic: '球隊攻防分析🔥🔥',
          link: '/forumdetail?id=nba2',
          image: 'https://picsum.photos/100/100',
          imagelink: '#',
          author: {
            name: '王大明',
            link: '#',
            date: '03-26 15:11'
          },
          latestReply: {
            author: '張宏偉',
            link: '#',
            date: '04-11 20:59'
          }
        },
        {
          topic: '近期勝率對比❤️❤️❤️',
          link: '/forumdetail?id=nba3',
          image: 'https://picsum.photos/100/100',
          imagelink: '#',
          author: {
            name: '陳小龍',
            link: '#',
            date: '04-05 01:52'
          },
          latestReply: {
            author: '吳嘉宏',
            link: '#',
            date: '04-11 20:59'
          }
        },
        {
          topic: '明星球員表現',
          link: '/forumdetail?id=nba4',
          image: 'https://picsum.photos/100/100',
          imagelink: '#',
          author: {
            name: '李佳穎',
            link: '#',
            date: '04-01 13:40'
          },
          latestReply: {
            author: '黃子傑',
            link: '#',
            date: '04-11 20:59'
          }
        },
        {
          topic: '最新比賽資訊⭐',
          link: '/forumdetail?id=nba5',
          image: 'https://picsum.photos/100/100',
          imagelink: '#',
          author: {
            name: '何俊傑',
            link: '#',
            date: '03-29 14:18'
          },
          latestReply: {
            author: '陳志強',
            link: '#',
            date: '04-11 20:59'
          }
        },
        {
          topic: '專家分析推薦',
          link: '/forumdetail?id=nba6',
          image: 'https://picsum.photos/100/100',
          imagelink: '#',
          author: {
            name: '周采妮',
            link: '#',
            date: '03-20 19:15'
          },
          latestReply: {
            author: '李秀華',
            link: '#',
            date: '04-11 20:59'
          }
        },
        {
          topic: '球隊近況解析',
          link: '/forumdetail?id=mlb1',
          image: 'https://picsum.photos/100/100',
          imagelink: '#',
          author: {
            name: '鄭文豪',
            link: '#',
            date: '03-20 19:15'
          },
          latestReply: {
            author: '林志明',
            link: '#',
            date: '04-11 20:59'
          }
        },
        {
          topic: '投手與打者數據⭐⭐',
          link: '/forumdetail?id=mlb2',
          image: 'https://picsum.photos/100/100',
          imagelink: '#',
          author: {
            name: '許佩珊',
            link: '#',
            date: '03-20 19:15'
          },
          latestReply: {
            author: '王晨宇',
            link: '#',
            date: '04-11 20:59'
          }
        },
        {
          topic: '近期排名與戰績🤩🤩',
          link: '/forumdetail?id=mlb3',
          image: 'https://picsum.photos/100/100',
          imagelink: '#',
          author: {
            name: '楊宗翰',
            link: '#',
            date: '03-20 19:15'
          },
          latestReply: {
            author: '李永豐',
            link: '#',
            date: '04-11 20:59'
          }
        },
        {
          topic: '大數據勝率分析🔥🔥🔥🔥🔥',
          link: '/forumdetail?id=mlb4',
          image: 'https://picsum.photos/100/100',
          imagelink: '#',
          author: {
            name: '林美玲',
            link: '#',
            date: '03-20 19:15'
          },
          latestReply: {
            author: '劉家祺',
            link: '#',
            date: '04-11 20:59'
          }
        },
        {
          topic: '球員表現分析',
          link: '/forumdetail?id=mlb5',
          image: 'https://picsum.photos/100/100',
          imagelink: '#',
          author: {
            name: '陳志明',
            link: '#',
            date: '03-20 19:15'
          },
          latestReply: {
            author: '朱亦賢',
            link: '#',
            date: '04-11 20:59'
          }
        },
  
      ];
      return {
        tableData
      };
    }
  });
  </script>
  
  <style scoped>
  .container {
    max-width: 1000px;
  }
  </style>
  