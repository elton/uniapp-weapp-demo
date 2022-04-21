<script setup>
  import { name, version } from '../package.json';
  import { onLaunch, onShow, onHide } from '@dcloudio/uni-app';

  onLaunch(() => {
    console.log(
      `%c ${name} %c v${version} `,
      'background:#35495e ; padding: 1px; border-radius: 3px 0 0 3px;  color: #fff',
      'background:#007aff ;padding: 1px; border-radius: 0 3px 3px 0;  color: #fff; font-weight: bold;'
    );
    console.log('App Launch');
  });

  onShow(() => {
    console.log('App Show');
  });

  onHide(() => {
    console.log('App Hide');
  });
</script>

<style>
  /*每个页面公共css */
  @import 'tailwindcss/base';
  @import 'tailwindcss/utilities';
</style>
