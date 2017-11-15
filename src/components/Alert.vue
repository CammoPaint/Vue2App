<template>
    <div class="alert-wrapper">
        <uiv-alert v-for="(alert, index) in alerts" :type="alert.type"  :duration="alert.duration" :key="alert.key" @dismissed="alerts.splice(index, 1)">
        <strong>{{alert.title}}:</strong> {{alert.msg}}
        </uiv-alert>
    </div>
</template>

<script>
export default {
  name: 'alert',
  props: ['alerts']
}
</script>