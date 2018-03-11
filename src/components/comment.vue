<template>
  <div class="comment">
    <button type="button" class="btn btn-agree float-left" @click="handlerAgree">
      <i class="icon icon-agree"></i>
      <span>{{ item.praise_count }}</span>
    </button>
    <div class="float-right">
      <button type="button" class="btn btn-talk" @click="handlerTalk">
        <i class="icon icon-talk"></i>
        <span>{{ item.comment_count }}</span>
      </button>
      <button type="button" class="btn btn-share">
        <i class="icon icon-share"></i>
        <span>{{ item.visit_count }}</span>
      </button>
    </div>
    <transition name="fade">
      <div class="input-box" v-show="inputShow">
        <input type="text" class="input" @blur="handleBlur" ref="input">
        <span class="send">发送</span>
      </div>
    </transition>
  </div>
</template>

<script>
  let once = false;
  export default {
    name: "comment",
    props: ['item'],
    data() {
      return {
        inputShow: false
      }
    },
    methods: {
      handlerAgree() {
        once ? this.item.praise_count-- : this.item.praise_count++;
        once = !once;
      },
      handlerTalk() {
        this.inputShow=true;
        setTimeout(()=>{
          this.$refs.input.focus()
        });
      },
      handleBlur() {
        this.inputShow=false;
      }
    }
  }
</script>

<style scoped lang="scss">
  $primary: #2887f0;
  .comment {
    position: relative;
    &::after {
      display: block;
      clear: both;
      content: "";
    }
  }

  .float-left {
    float: left;
  }

  .float-right {
    float: right;
  }

  .btn {
    background-color: transparent;
    color: #737373;
    padding: 3px 10px;
    border: none;
    line-height: 0;
    span {
      line-height: 20px;
      display: inline-block;
      vertical-align: super;
    }
  }

  .btn-agree {
    border: 1px solid #cdcdcd;
    border-radius: 0.8rem;
  }

  .icon {
    display: inline-block;
    width: 20px;
    height: 20px;
    background-size: 20px;
    &.icon-agree {
      background: url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9Im5vIj8+Cjxzdmcgd2lkdGg9IjI0cHgiIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB2ZXJzaW9uPSIxLjEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiPgogICAgPCEtLSBHZW5lcmF0b3I6IFNrZXRjaCA0MC4yICgzMzgyNikgLSBodHRwOi8vd3d3LmJvaGVtaWFuY29kaW5nLmNvbS9za2V0Y2ggLS0+CiAgICA8dGl0bGU+54K56LWePC90aXRsZT4KICAgIDxkZXNjPkNyZWF0ZWQgd2l0aCBTa2V0Y2guPC9kZXNjPgogICAgPGRlZnM+CiAgICAgICAgPHBvbHlnb24gaWQ9InBhdGgtMSIgcG9pbnRzPSI0LjUzMzMzMzMzIDYgMy40IDYgMy40IDE0LjczMzMzMzMgNC41MzMzMzMzMyAxNC43MzMzMzMzIj48L3BvbHlnb24+CiAgICAgICAgPG1hc2sgaWQ9Im1hc2stMiIgbWFza0NvbnRlbnRVbml0cz0idXNlclNwYWNlT25Vc2UiIG1hc2tVbml0cz0ib2JqZWN0Qm91bmRpbmdCb3giIHg9IjAiIHk9IjAiIHdpZHRoPSIxLjEzMzMzMzMzIiBoZWlnaHQ9IjguNzMzMzMzMzMiIGZpbGw9IndoaXRlIj4KICAgICAgICAgICAgPHVzZSB4bGluazpocmVmPSIjcGF0aC0xIj48L3VzZT4KICAgICAgICA8L21hc2s+CiAgICAgICAgPHBhdGggZD0iTTMuOTY2NjY2NjcsMTUuMyBMMS4xMzMzMzMzMywxNS4zIEMwLjUwNzE2NjY2NywxNS4zIDAsMTQuNzkyODMzMyAwLDE0LjE2NjY2NjcgTDAsNi44IEMwLDYuMTczODMzMzMgMC41MDcxNjY2NjcsNS42NjY2NjY2NyAxLjEzMzMzMzMzLDUuNjY2NjY2NjcgTDMuOTY2NjY2NjcsNS42NjY2NjY2NyBDNC4zODM3MzMzMyw1LjY2NjY2NjY3IDQuNzQ0Nyw1Ljg5NDQ2NjY3IDQuOTQxMzMzMzMsNi4yMzA1IEM0Ljk5NzQzMzMzLDYuMjMxMDY2NjcgNS4wNTEyNjY2Nyw2LjIzMjIgNS4xLDYuMjMzMzMzMzMgQzYuNjA0NSw2LjI2Njc2NjY3IDYuODgzMyw0LjY1NTczMzMzIDcuMjYzNTMzMzMsMy40MDc5MzMzMyBDOC4wMjU3LDAuOTA3MjMzMzMzIDcuMzc2ODY2NjcsMCA5LjA2NjY2NjY3LDAgQzExLjIzMTMzMzMsMCAxMS45MjIxLDEuMjI3OTY2NjcgMTEuOSwyLjgzMzMzMzMzIEMxMS44Nzc5LDQuNDMxOSAxMC42OTI0MzMzLDUuNjExNyAxMi40NjY2NjY3LDUuNjY2NjY2NjcgTDE0LjE2NjY2NjcsNS42NjY2NjY2NyBDMTUuOTI2NzMzMyw1LjU5MDczMzMzIDE2Ljk3NzksNi40NjA1NjY2NyAxNi40MzMzMzMzLDkuMDY2NjY2NjcgQzE2LjExMDMzMzMsMTAuNjEyNTMzMyAxNS45NTIyMzMzLDExLjI2NDIgMTUuMywxMy42IEMxNC44NzYxMzMzLDE1LjExOTIzMzMgMTMuNzg5ODMzMywxNS44NjY2NjY3IDExLjksMTUuODY2NjY2NyBDMTAuMDEwMTY2NywxNS44NjY2NjY3IDguNDQyNzY2NjcsMTUuODI5MjY2NyA3LjM2NjY2NjY3LDE1Ljg2NjY2NjcgQzYuMjk3OTMzMzMsMTUuOTA0MDY2NyA2LjUzNDgsMTQuNzMzOSA1LjEsMTQuNzMzMzMzMyBMNC45NDMwMzMzMywxNC43MzMzMzMzIEM0Ljc0NTgzMzMzLDE1LjA3MDUgNC4zODU0MzMzMywxNS4yOTk0MzMzIDMuOTY2NjY2NjcsMTUuMyBMMy45NjY2NjY2NywxNS4zIFoiIGlkPSJwYXRoLTMiPjwvcGF0aD4KICAgICAgICA8bWFzayBpZD0ibWFzay00IiBtYXNrQ29udGVudFVuaXRzPSJ1c2VyU3BhY2VPblVzZSIgbWFza1VuaXRzPSJvYmplY3RCb3VuZGluZ0JveCIgeD0iMCIgeT0iMCIgd2lkdGg9IjE2LjU3NzQ2NjgiIGhlaWdodD0iMTUuODY3NTQ0NCIgZmlsbD0id2hpdGUiPgogICAgICAgICAgICA8dXNlIHhsaW5rOmhyZWY9IiNwYXRoLTMiPjwvdXNlPgogICAgICAgIDwvbWFzaz4KICAgIDwvZGVmcz4KICAgIDxnIGlkPSJTeW1ib2xzIiBzdHJva2U9Im5vbmUiIHN0cm9rZS13aWR0aD0iMSIgZmlsbD0ibm9uZSIgZmlsbC1ydWxlPSJldmVub2RkIj4KICAgICAgICA8ZyBpZD0i5paH56ug5qCPIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtNTQwLjAwMDAwMCwgLTc2LjAwMDAwMCkiIHN0cm9rZT0iI0FBQUFBQSI+CiAgICAgICAgICAgIDxnIGlkPSJHcm91cCI+CiAgICAgICAgICAgICAgICA8ZyBpZD0iR3JvdXAtMiIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMTk4LjAwMDAwMCwgNzYuMDAwMDAwKSI+CiAgICAgICAgICAgICAgICAgICAgPGcgaWQ9IueCuei1niIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMzQ2LjAwMDAwMCwgMy4wMDAwMDApIj4KICAgICAgICAgICAgICAgICAgICAgICAgPHVzZSBpZD0iXy0tcGF0aCIgbWFzaz0idXJsKCNtYXNrLTIpIiBzdHJva2Utd2lkdGg9IjQiIHhsaW5rOmhyZWY9IiNwYXRoLTEiPjwvdXNlPgogICAgICAgICAgICAgICAgICAgICAgICA8dXNlIGlkPSJfLS1wYXRoIiBtYXNrPSJ1cmwoI21hc2stNCkiIHN0cm9rZS13aWR0aD0iMiIgeGxpbms6aHJlZj0iI3BhdGgtMyI+PC91c2U+CiAgICAgICAgICAgICAgICAgICAgPC9nPgogICAgICAgICAgICAgICAgPC9nPgogICAgICAgICAgICA8L2c+CiAgICAgICAgPC9nPgogICAgPC9nPgo8L3N2Zz4=) center no-repeat;
    }
    &.icon-talk {
      background: url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9Im5vIj8+Cjxzdmcgd2lkdGg9IjI0cHgiIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB2ZXJzaW9uPSIxLjEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiPgogICAgPCEtLSBHZW5lcmF0b3I6IFNrZXRjaCA0MC4yICgzMzgyNikgLSBodHRwOi8vd3d3LmJvaGVtaWFuY29kaW5nLmNvbS9za2V0Y2ggLS0+CiAgICA8dGl0bGU+6K+E6K66PC90aXRsZT4KICAgIDxkZXNjPkNyZWF0ZWQgd2l0aCBTa2V0Y2guPC9kZXNjPgogICAgPGRlZnM+CiAgICAgICAgPHBhdGggZD0iTTguODQyMTA1MjYsMTMuNjkxMDc2OSBDNy40OTYzMzY4NCwxMy42OTEwNzY5IDUuNDIzMTU3ODksMTIuODUwMzk2OCAzLjQzODQsMTUuMTU3ODk0NyBDMy44MTMzMDUyNiwxMy41NDc2NTk5IDMuNDgyMDIxMDUsMTIuMzM1NjExMyAyLjgxNTMyNjMyLDExLjg1NDYzOTcgQzEuMDgzNDUyNjMsMTAuNjA0Njk2NCAwLDguODIzMDYwNzMgMCw2Ljg0NTUzODQ2IEMwLDMuMDY0ODA5NzIgMy45NTg5MDUyNiwwIDguODQyMTA1MjYsMCBDMTMuNzI1MzA1MywwIDE3LjY4NDIxMDUsMy4wNjQ4MDk3MiAxNy42ODQyMTA1LDYuODQ1NTM4NDYgQzE3LjY4NDIxMDUsMTAuNjI2MjY3MiAxMy43MjUzMDUzLDEzLjY5MTA3NjkgOC44NDIxMDUyNiwxMy42OTEwNzY5IEw4Ljg0MjEwNTI2LDEzLjY5MTA3NjkgWiIgaWQ9InBhdGgtMSI+PC9wYXRoPgogICAgICAgIDxtYXNrIGlkPSJtYXNrLTIiIG1hc2tDb250ZW50VW5pdHM9InVzZXJTcGFjZU9uVXNlIiBtYXNrVW5pdHM9Im9iamVjdEJvdW5kaW5nQm94IiB4PSIwIiB5PSIwIiB3aWR0aD0iMTcuNjg0MjEwNSIgaGVpZ2h0PSIxNS4xNTc4OTQ3IiBmaWxsPSJ3aGl0ZSI+CiAgICAgICAgICAgIDx1c2UgeGxpbms6aHJlZj0iI3BhdGgtMSI+PC91c2U+CiAgICAgICAgPC9tYXNrPgogICAgPC9kZWZzPgogICAgPGcgaWQ9IlN5bWJvbHMiIHN0cm9rZT0ibm9uZSIgc3Ryb2tlLXdpZHRoPSIxIiBmaWxsPSJub25lIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiPgogICAgICAgIDxnIGlkPSLmlofnq6DmoI8iIHRyYW5zZm9ybT0idHJhbnNsYXRlKC02NDIuMDAwMDAwLCAtNzYuMDAwMDAwKSI+CiAgICAgICAgICAgIDxnIGlkPSJHcm91cCI+CiAgICAgICAgICAgICAgICA8ZyBpZD0iR3JvdXAtMiIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMTk4LjAwMDAwMCwgNzYuMDAwMDAwKSI+CiAgICAgICAgICAgICAgICAgICAgPGcgaWQ9IuivhOiuuiIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoNDQ3LjAwMDAwMCwgNS4wMDAwMDApIj4KICAgICAgICAgICAgICAgICAgICAgICAgPHBhdGggZD0iTTEzLjA1MjYzMTYsNS44OTQ3MzY4NCBDMTIuMzU1MzY4NCw1Ljg5NDczNjg0IDExLjc4OTQ3MzcsNi40NTk5Mzc1NyAxMS43ODk0NzM3LDcuMTU3ODk0NzQgQzExLjc4OTQ3MzcsNy44NTUxOTQ3IDEyLjM1NTM2ODQsOC40MjEwNTI2MyAxMy4wNTI2MzE2LDguNDIxMDUyNjMgQzEzLjc1MDU2ODQsOC40MjEwNTI2MyAxNC4zMTU3ODk1LDcuODU1MTk0NyAxNC4zMTU3ODk1LDcuMTU3ODk0NzQgQzE0LjMxNTc4OTUsNi40NTk5Mzc1NyAxMy43NTA1Njg0LDUuODk0NzM2ODQgMTMuMDUyNjMxNiw1Ljg5NDczNjg0IFogTTguODQyMTA1MjYsNS44OTQ3MzY4NCBDOC4xNDQxNjg0Miw1Ljg5NDczNjg0IDcuNTc4OTQ3MzcsNi40NTk5Mzc1NyA3LjU3ODk0NzM3LDcuMTU3ODk0NzQgQzcuNTc4OTQ3MzcsNy44NTUxOTQ3IDguMTQ0MTY4NDIsOC40MjEwNTI2MyA4Ljg0MjEwNTI2LDguNDIxMDUyNjMgQzkuNTQwMDQyMTEsOC40MjEwNTI2MyAxMC4xMDUyNjMyLDcuODU1MTk0NyAxMC4xMDUyNjMyLDcuMTU3ODk0NzQgQzEwLjEwNTI2MzIsNi40NTk5Mzc1NyA5LjU0MDA0MjExLDUuODk0NzM2ODQgOC44NDIxMDUyNiw1Ljg5NDczNjg0IFogTTQuNjMxNTc4OTUsNS44OTQ3MzY4NCBDMy45MzM2NDIxMSw1Ljg5NDczNjg0IDMuMzY4NDIxMDUsNi40NTk5Mzc1NyAzLjM2ODQyMTA1LDcuMTU3ODk0NzQgQzMuMzY4NDIxMDUsNy44NTUxOTQ3IDMuOTMzNjQyMTEsOC40MjEwNTI2MyA0LjYzMTU3ODk1LDguNDIxMDUyNjMgQzUuMzI5NTE1NzksOC40MjEwNTI2MyA1Ljg5NDczNjg0LDcuODU1MTk0NyA1Ljg5NDczNjg0LDcuMTU3ODk0NzQgQzUuODk0NzM2ODQsNi40NTk5Mzc1NyA1LjMyOTUxNTc5LDUuODk0NzM2ODQgNC42MzE1Nzg5NSw1Ljg5NDczNjg0IFoiIGlkPSJDb21iaW5lZC1TaGFwZSIgZmlsbD0iI0FBQUFBQSI+PC9wYXRoPgogICAgICAgICAgICAgICAgICAgICAgICA8dXNlIGlkPSJfLS0xLXBhdGgiIHN0cm9rZT0iI0FBQUFBQSIgbWFzaz0idXJsKCNtYXNrLTIpIiBzdHJva2Utd2lkdGg9IjIiIHhsaW5rOmhyZWY9IiNwYXRoLTEiPjwvdXNlPgogICAgICAgICAgICAgICAgICAgIDwvZz4KICAgICAgICAgICAgICAgIDwvZz4KICAgICAgICAgICAgPC9nPgogICAgICAgIDwvZz4KICAgIDwvZz4KPC9zdmc+) center no-repeat;
    }
    &.icon-share {
      background: url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9Im5vIj8+Cjxzdmcgd2lkdGg9IjI0cHgiIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB2ZXJzaW9uPSIxLjEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiPgogICAgPCEtLSBHZW5lcmF0b3I6IFNrZXRjaCA0MC4yICgzMzgyNikgLSBodHRwOi8vd3d3LmJvaGVtaWFuY29kaW5nLmNvbS9za2V0Y2ggLS0+CiAgICA8dGl0bGU+5p+l55yLPC90aXRsZT4KICAgIDxkZXNjPkNyZWF0ZWQgd2l0aCBTa2V0Y2guPC9kZXNjPgogICAgPGRlZnM+CiAgICAgICAgPHBhdGggZD0iTTEwLDEzLjMzMzMzMzMgQzUuNTc4ODg4ODksMTMuMzMzMzMzMyAyLjE3Mzg4ODg5LDEwLjIzMjc3NzggMCw2LjY2NjY2NjY3IEMyLjE3Mzg4ODg5LDMuMTAwNTU1NTYgNS41Nzg4ODg4OSwwIDEwLDAgQzE0LjQyMTExMTEsMCAxNy44MjYxMTExLDMuMTAwNTU1NTYgMjAsNi42NjY2NjY2NyBDMTcuODI2MTExMSwxMC4yMzI3Nzc4IDE0LjQyMTExMTEsMTMuMzMzMzMzMyAxMCwxMy4zMzMzMzMzIEwxMCwxMy4zMzMzMzMzIFoiIGlkPSJwYXRoLTEiPjwvcGF0aD4KICAgICAgICA8bWFzayBpZD0ibWFzay0yIiBtYXNrQ29udGVudFVuaXRzPSJ1c2VyU3BhY2VPblVzZSIgbWFza1VuaXRzPSJvYmplY3RCb3VuZGluZ0JveCIgeD0iMCIgeT0iMCIgd2lkdGg9IjIwIiBoZWlnaHQ9IjEzLjMzMzMzMzMiIGZpbGw9IndoaXRlIj4KICAgICAgICAgICAgPHVzZSB4bGluazpocmVmPSIjcGF0aC0xIj48L3VzZT4KICAgICAgICA8L21hc2s+CiAgICA8L2RlZnM+CiAgICA8ZyBpZD0iU3ltYm9scyIgc3Ryb2tlPSJub25lIiBzdHJva2Utd2lkdGg9IjEiIGZpbGw9Im5vbmUiIGZpbGwtcnVsZT0iZXZlbm9kZCI+CiAgICAgICAgPGcgaWQ9IuaWh+eroOagjyIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTQzOC4wMDAwMDAsIC03Ni4wMDAwMDApIiBzdHJva2U9IiNBQUFBQUEiPgogICAgICAgICAgICA8ZyBpZD0iR3JvdXAiPgogICAgICAgICAgICAgICAgPGcgaWQ9Ikdyb3VwLTIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDE5OC4wMDAwMDAsIDc2LjAwMDAwMCkiPgogICAgICAgICAgICAgICAgICAgIDxnIGlkPSLpmIXor7siIHRyYW5zZm9ybT0idHJhbnNsYXRlKDI0Mi4wMDAwMDAsIDYuMDAwMDAwKSI+CiAgICAgICAgICAgICAgICAgICAgICAgIDxwYXRoIGQ9Ik0xMCwwLjkgQzcuNDg2NjY2NjcsMC45IDUuNDQ5NDQ0NDQsMi45ODQ0NDQ0NCA1LjQ0OTQ0NDQ0LDUuNTU1NTU1NTYgQzUuNDQ5NDQ0NDQsOC4xMjY2NjY2NyA3LjQ4NjY2NjY3LDEwLjIxMTExMTEgMTAsMTAuMjExMTExMSBDMTIuNTEzMzMzMywxMC4yMTExMTExIDE0LjU1MDU1NTYsOC4xMjY2NjY2NyAxNC41NTA1NTU2LDUuNTU1NTU1NTYgQzE0LjU1MDU1NTYsMi45ODQ0NDQ0NCAxMi41MTMzMzMzLDAuOSAxMCwwLjkgTDEwLDAuOSBaIiBpZD0iXy0tMi1wYXRoIj48L3BhdGg+CiAgICAgICAgICAgICAgICAgICAgICAgIDx1c2UgaWQ9Il8tLTItcGF0aCIgbWFzaz0idXJsKCNtYXNrLTIpIiBzdHJva2Utd2lkdGg9IjIiIHhsaW5rOmhyZWY9IiNwYXRoLTEiPjwvdXNlPgogICAgICAgICAgICAgICAgICAgIDwvZz4KICAgICAgICAgICAgICAgIDwvZz4KICAgICAgICAgICAgPC9nPgogICAgICAgIDwvZz4KICAgIDwvZz4KPC9zdmc+) center no-repeat;
    }
  }

  .input-box {
    position: absolute;
    width: 100%;
    left: 0;
    display: flex;
    background-color: #fff;
    .input {
      padding: 4px 10px;
      height: 20px;
      border: 1px solid #cdcdcd;
      border-radius: 0.8rem;
      flex: 1;
    }
    .send {
      color: $primary;
      font-weight: 700;
      margin: 5px 6px;
      cursor: pointer;
    }
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
  }

  .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */
  {
    opacity: 0;
  }
</style>
