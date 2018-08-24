<template>
  <div>
    <a
      :href="href"
      v-bind:style="style"
    >
      <!-- Dynamic src leads to placing actual path into html, but we want it to compile into data:image. -->
      <template v-if="light">
        <img src="../assets/GitHub-Mark-Light-32px.png" alt="GitHub" />
      </template>
      <template v-else>
        <img src="../assets/GitHub-Mark-32px.png" alt="GitHub" />
      </template>
    </a>
  </div>
</template>

<script>
export default {
  name: 'GithubMark',
  props: {
    href: String,
    position: String,
    light: Boolean,
  },
  computed: {
    style: function () {
      const position = this.position || 'bottom-right'
      const padding = this.padding || '8px-8px'

      const propSplitRegExp = /([^-]+)-([^-]+)/
      const parsedPosition = position.match(propSplitRegExp)
      const parsedPadding = padding.match(propSplitRegExp)

      const styleProps = {
        zIndex: '9999',
        position: 'fixed',
        width: '32px',
        height: '32px',
      }

      if (parsedPosition && parsedPadding) {
        styleProps[parsedPosition[1]] = parsedPadding[1]
        styleProps[parsedPosition[2]] = parsedPadding[2]
      }

      return styleProps
    },
  },
}
</script>
