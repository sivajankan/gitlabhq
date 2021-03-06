<script>

/* This is a re-usable vue component for rendering a user avatar that
  does not need to link to the user's profile. The image and an optional
  tooltip can be configured by props passed to this component.

  Sample configuration:

  <user-avatar-image
    :img-src="userAvatarSrc"
    :img-alt="tooltipText"
    :tooltip-text="tooltipText"
    tooltip-placement="top"
  />

*/

import defaultAvatarUrl from 'images/no_avatar.png';
import tooltip from '../../directives/tooltip';

export default {
  name: 'UserAvatarImage',
  props: {
    imgSrc: {
      type: String,
      required: false,
      default: defaultAvatarUrl,
    },
    cssClasses: {
      type: String,
      required: false,
      default: '',
    },
    imgAlt: {
      type: String,
      required: false,
      default: 'user avatar',
    },
    size: {
      type: Number,
      required: false,
      default: 20,
    },
    tooltipText: {
      type: String,
      required: false,
      default: '',
    },
    tooltipPlacement: {
      type: String,
      required: false,
      default: 'top',
    },
  },
  directives: {
    tooltip,
  },
  computed: {
    tooltipContainer() {
      return this.tooltipText ? 'body' : null;
    },
    avatarSizeClass() {
      return `s${this.size}`;
    },
    // API response sends null when gravatar is disabled and
    // we provide an empty string when we use it inside user avatar link.
    // In both cases we should render the defaultAvatarUrl
    imageSource() {
      return this.imgSrc === '' || this.imgSrc === null ? defaultAvatarUrl : this.imgSrc;
    },
  },
};
</script>

<template>
  <img
    v-tooltip
    class="avatar"
    :class="[avatarSizeClass, cssClasses]"
    :src="imageSource"
    :width="size"
    :height="size"
    :alt="imgAlt"
    :data-container="tooltipContainer"
    :data-placement="tooltipPlacement"
    :title="tooltipText"
  />
</template>
