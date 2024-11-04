<script lang="ts" setup>
import { Icon } from '@iconify/vue';
import { computed, ref } from 'vue';

// Components
import newFooter from '@/layouts/components/NavFooter.vue';
import NavbarThemeSwitcher from '@/layouts/components/NavbarThemeSwitcher.vue';
import NavbarSearch from '@/layouts/components/NavbarSearch.vue';
import ChainProfile from '@/layouts/components/ChainProfile.vue';
import Sponsors from '@/layouts/components/Sponsors.vue';

import { NetworkType, useDashboard } from '@/stores/useDashboard';
import { useBaseStore, useBlockchain } from '@/stores';

import NavBarI18n from './NavBarI18n.vue';
import NavBarWallet from './NavBarWallet.vue';
import type { NavGroup, NavLink, NavSectionTitle, VerticalNavItems } from '../types';
import dayjs from 'dayjs';

const dashboard = useDashboard();
dashboard.initial();
const blockchain = useBlockchain();
blockchain.randomSetupEndpoint();
const baseStore = useBaseStore();

const current = ref(''); // the current chain
const temp = ref('')
blockchain.$subscribe((m, s) => {
  if(current.value ===s.chainName && temp.value != s.endpoint.address) {
    temp.value = s.endpoint.address
    blockchain.initial();
  }
  if (current.value != s.chainName) {
    current.value = s.chainName;
    blockchain.randomSetupEndpoint();
  }
});

const sidebarShow = ref(false);
const sidebarOpen = ref(true);

const changeOpen = (index: Number) => {
  if (index === 0) {
    sidebarOpen.value = !sidebarOpen.value;
  }
};
const showDiscord = window.location.host.search('ping.pub') > -1;

function isNavGroup(nav: VerticalNavItems | any): nav is NavGroup {
   return (<NavGroup>nav).children !== undefined;
}
function isNavLink(nav: VerticalNavItems | any): nav is NavLink {
   return (<NavLink>nav).to !== undefined;
}
function isNavTitle(nav: VerticalNavItems | any): nav is NavSectionTitle {
   return (<NavSectionTitle>nav).heading !== undefined;
}
function selected(route: any, nav: NavLink) {
  const b = route.path === nav.to?.path || route.path.startsWith(nav.to?.path) && nav.title.indexOf('dashboard') === -1
  return b
}
const blocktime = computed(() => {
  return dayjs(baseStore.latest?.block?.header?.time)
});

const behind = computed(() => {
  const current = dayjs().subtract(10, 'minute')
  return blocktime.value.isBefore(current)
});

dayjs()

</script>

<template>
  <div class="bg-gray-100 dark:bg-[#171d30]">
    <!-- sidebar -->
    <div
      class="w-64 fixed z-50 left-0 top-0 bottom-0 overflow-auto bg-base-100 border-r border-gray-100 dark:border-gray-700"
      :class="{ block: sidebarShow, 'hidden xl:!block': !sidebarShow }"
    >
      <div class="flex justify-center mt-1 pl-4 py-4 mb-1">
        <RouterLink to="/" class="flex items-center">
          <!-- <img class="w-10 h-10" src="../../assets/logo.svg" /> -->
          <svg
            viewBox="0 0 183.32678 52.126812"
            version="1.1"
            id="svg169"
            sodipodi:docname="neobase-logo-horizontal.svg"
            width="183.3268"
            height="52.126812"
            inkscape:version="1.1 (c4e8f9e, 2021-05-24)"
            xmlns:inkscape="http://www.inkscape.org/namespaces/inkscape"
            xmlns:sodipodi="http://sodipodi.sourceforge.net/DTD/sodipodi-0.dtd"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:svg="http://www.w3.org/2000/svg"
            xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
            xmlns:cc="http://creativecommons.org/ns#"
            xmlns:dc="http://purl.org/dc/elements/1.1/"
          >
            <sodipodi:namedview
              id="namedview171"
              pagecolor="#ffffff"
              bordercolor="#666666"
              borderopacity="1.0"
              inkscape:pageshadow="2"
              inkscape:pageopacity="0.0"
              inkscape:pagecheckerboard="0"
              showgrid="false"
              fit-margin-top="0"
              fit-margin-left="0"
              fit-margin-right="0"
              fit-margin-bottom="0"
              inkscape:zoom="3.7572545"
              inkscape:cx="58.952621"
              inkscape:cy="40.854299"
              inkscape:window-width="1312"
              inkscape:window-height="847"
              inkscape:window-x="0"
              inkscape:window-y="25"
              inkscape:window-maximized="0"
              inkscape:current-layer="svg169"
            />
            <defs id="defs119">
              <linearGradient
                id="a"
                x1="1.28"
                y1="164.53"
                x2="258.89001"
                y2="164.53"
                gradientUnits="userSpaceOnUse"
              >
                <stop offset="0" stop-color="gold" id="stop99" />
                <stop offset="0.02" stop-color="#fcd403" id="stop101" />
                <stop offset="0.22" stop-color="#e6be19" id="stop103" />
                <stop offset="0.43" stop-color="#d7ad29" id="stop105" />
                <stop offset="0.68" stop-color="#cea432" id="stop107" />
                <stop offset="1" stop-color="#cba135" id="stop109" />
              </linearGradient>
              <linearGradient
                id="b"
                x1="24.75"
                y1="163.06"
                x2="282.35001"
                y2="163.06"
                xlink:href="#a"
                gradientTransform="matrix(0.16189021,0,0,0.15648059,-0.20721946,0)"
              />
              <linearGradient
                id="c"
                x1="76"
                y1="99.07"
                x2="212.99001"
                y2="233.78"
                xlink:href="#a"
              />
              <linearGradient
                id="d"
                x1="56.950001"
                y1="324.82999"
                x2="259.85001"
                y2="424.78"
                gradientUnits="userSpaceOnUse"
              >
                <stop offset="0" stop-color="gold" id="stop114" />
                <stop offset="1" stop-color="#cba135" id="stop116" />
              </linearGradient>
              <linearGradient
                inkscape:collect="always"
                xlink:href="#d"
                id="linearGradient253"
                gradientUnits="userSpaceOnUse"
                x1="56.950001"
                y1="324.82999"
                x2="259.85001"
                y2="424.78"
                gradientTransform="matrix(0.45604699,0,0,0.44080802,54.384886,-133.87103)"
              />
              <linearGradient
                inkscape:collect="always"
                xlink:href="#d"
                id="linearGradient255"
                gradientUnits="userSpaceOnUse"
                x1="56.950001"
                y1="324.82999"
                x2="259.85001"
                y2="424.78"
                gradientTransform="matrix(0.45604699,0,0,0.44080802,54.384886,-133.87103)"
              />
              <linearGradient
                inkscape:collect="always"
                xlink:href="#d"
                id="linearGradient257"
                gradientUnits="userSpaceOnUse"
                x1="56.950001"
                y1="324.82999"
                x2="259.85001"
                y2="424.78"
                gradientTransform="matrix(0.45604699,0,0,0.44080802,54.384886,-133.87103)"
              />
              <linearGradient
                inkscape:collect="always"
                xlink:href="#d"
                id="linearGradient259"
                gradientUnits="userSpaceOnUse"
                x1="56.950001"
                y1="324.82999"
                x2="259.85001"
                y2="424.78"
                gradientTransform="matrix(0.45604699,0,0,0.44080802,54.384886,-133.87103)"
              />
              <linearGradient
                inkscape:collect="always"
                xlink:href="#d"
                id="linearGradient261"
                gradientUnits="userSpaceOnUse"
                x1="56.950001"
                y1="324.82999"
                x2="259.85001"
                y2="424.78"
                gradientTransform="matrix(0.45604699,0,0,0.44080802,54.384886,-133.87103)"
              />
              <linearGradient
                inkscape:collect="always"
                xlink:href="#d"
                id="linearGradient263"
                gradientUnits="userSpaceOnUse"
                x1="56.950001"
                y1="324.82999"
                x2="259.85001"
                y2="424.78"
                gradientTransform="matrix(0.45604699,0,0,0.44080802,54.384886,-133.87103)"
              />
              <linearGradient
                inkscape:collect="always"
                xlink:href="#d"
                id="linearGradient265"
                gradientUnits="userSpaceOnUse"
                x1="56.950001"
                y1="324.82999"
                x2="259.85001"
                y2="424.78"
                gradientTransform="matrix(0.45604699,0,0,0.44080802,54.384886,-133.87103)"
              />
              <linearGradient
                inkscape:collect="always"
                xlink:href="#a"
                id="linearGradient267"
                gradientUnits="userSpaceOnUse"
                x1="1.28"
                y1="164.53"
                x2="258.89001"
                y2="164.53"
                gradientTransform="matrix(0.16189021,0,0,0.15648059,-0.20721946,0)"
              />
            </defs>
            <title id="title121">Neobase-gold-logo</title>
            <path
              d="m 7.8419615,18.530431 v 21.3596 H 3.9209805 V 4.0184216 L 0,0.23002642 V 43.681555 H 22.781189 L 18.85859,39.890031 H 11.772655 V 27.684544 l 3.304178,3.195334 0.615185,0.593061 0.86935,0.840302 15.683923,15.159839 h -16.56137 l 3.83842,3.791526 h 22.178957 z"
              style="fill: url(#linearGradient267); stroke-width: 0.159162"
              id="path129"
            />
            <path
              d="M 37.660518,32.731045 V 11.36988 h 3.922599 v 35.873174 l 3.919362,3.788394 V 7.5799198 H 22.731003 l 3.920982,3.7899602 h 7.087552 V 23.575365 L 13.266903,3.7915246 H 29.820175 L 25.98014,0 H 3.8011819 Z"
              style="fill: url(#b); stroke-width: 0.159162"
              id="path131"
            />
            <polygon
              points="237.88,275.86 46.91,84.73 45.75,51.72 236.73,242.86 "
              style="fill: url(#c)"
              id="polygon133"
              transform="matrix(0.1618902,0,0,0.15648059,-0.20721945,0)"
            />
            <path
              d="M 70.141297,36.615873 59.241775,24.295292 v 11.40811 a 1.3955036,1.3488725 0 1 1 -2.786446,0 v -15.03596 c 0,-1.040307 1.413746,-2.071798 2.640513,-0.683255 L 69.799261,32.084368 V 20.667442 a 1.3955036,1.3488725 0 1 1 2.786448,0 v 15.03596 a 1.4046246,1.3576886 0 0 1 -0.8072,1.221038 1.3681408,1.3224239 0 0 1 -1.637212,-0.308567 z"
              style="fill: url(#linearGradient253); stroke-width: 0.448362"
              id="path155"
            />
            <path
              d="m 90.129837,19.31416 v 2.812354 H 75.992381 V 19.31416 Z m 0,17.729298 H 75.992381 V 26.785855 h 14.137456 v 2.785906 H 78.888278 v 4.659342 h 11.241559 z"
              style="fill: url(#linearGradient255); stroke-width: 0.448362"
              id="path157"
            />
            <path
              d="m 112.03833,28.178807 a 9.6453926,9.3230883 0 1 1 -9.6454,-9.323086 9.6545133,9.3319049 0 0 1 9.6454,9.323086 z m -9.6454,-6.409346 a 6.6309223,6.4093479 0 1 0 6.63093,6.409346 6.6218013,6.400532 0 0 0 -6.63093,-6.409346 z"
              style="fill: url(#linearGradient257); stroke-width: 0.448362"
              id="path159"
            />
            <path
              d="m 125.92497,19.31416 a 5.2764629,5.1001482 0 0 1 3.56628,8.864647 5.2764629,5.1001482 0 0 1 -3.56628,8.864651 h -9.45386 a 1.3955036,1.3488725 0 0 1 -1.39551,-1.344464 v -7.520187 a 1.4000641,1.3532805 0 0 1 1.39551,-1.348872 h 9.45386 a 2.4945768,2.4112196 0 0 0 0,-4.822436 h -9.45386 a 1.3955036,1.3488725 0 1 1 0,-2.693339 z m 0,15.035961 a 2.4991374,2.4156278 0 1 0 0,-4.826847 h -8.05836 v 4.826847 z"
              style="fill: url(#linearGradient259); stroke-width: 0.448362"
              id="path161"
            />
            <path
              d="m 133.42236,35.165616 c 0.98507,-2.173186 6.15209,-14.480542 7.25116,-15.4944 a 1.2130848,1.1725491 0 0 1 0.81632,-0.357056 1.1948429,1.1549169 0 0 1 0.81633,0.357056 c 1.10362,1.013858 6.26608,13.321214 7.25114,15.4944 0.73424,1.622174 -1.82419,2.693337 -2.54474,1.075571 l -5.52273,-12.183934 -5.51817,12.183934 c -0.73424,1.617766 -3.28353,0.546603 -2.54931,-1.075571 z"
              style="fill: url(#linearGradient261); stroke-width: 0.448362"
              id="path163"
            />
            <path
              d="m 162.98334,23.113926 a 6.4439429,6.2286165 0 0 0 -4.50575,-1.547237 4.7064043,4.5491383 0 0 0 -1.5232,0.379095 2.9004585,2.8035389 0 0 0 -1.0489,0.762598 2.3440814,2.2657531 0 0 0 -0.54727,1.719151 c 0.25995,1.419401 2.22551,1.979228 4.19107,2.508198 3.25161,0.912471 6.47132,1.798496 6.07912,5.955315 v 0.02204 a 5.130528,4.9590897 0 0 1 -1.04892,2.406812 6.065424,5.8627462 0 0 1 -2.82749,1.798494 8.4824726,8.1990284 0 0 1 -3.67117,0.255671 12.769315,12.342624 0 0 1 -6.47131,-2.785906 l 1.82418,-2.20404 a 10.033033,9.6977757 0 0 0 4.98916,2.133511 5.6139379,5.4263461 0 0 0 2.4353,-0.149877 2.8320513,2.7374175 0 0 0 1.4183,-0.881614 1.8241877,1.7632319 0 0 0 0.41955,-0.934513 c 0.1277,-1.763233 -1.88803,-2.331875 -3.95849,-2.913741 -2.90956,-0.784638 -5.84194,-1.622173 -6.31623,-4.941458 v -0.101383 a 5.4725633,5.2896956 0 0 1 1.23132,-3.773316 6.3846574,6.1713116 0 0 1 2.04309,-1.49434 7.7163141,7.4584708 0 0 1 2.57211,-0.634763 9.3170383,9.0057065 0 0 1 6.60355,2.20404 z"
              style="fill: url(#linearGradient263); stroke-width: 0.448362"
              id="path165"
            />
            <path
              d="m 182.42917,19.31416 v 2.812354 H 168.29172 V 19.31416 Z m 0,17.729298 H 168.29172 V 26.785855 h 14.13745 v 2.785906 h -11.24611 v 4.659342 h 11.24611 z"
              style="fill: url(#linearGradient265); stroke-width: 0.448362"
              id="path167"
            />
            <metadata id="metadata271">
              <rdf:RDF>
                <cc:Work rdf:about="">
                  <dc:title>Neobase-gold-logo</dc:title>
                </cc:Work>
              </rdf:RDF>
            </metadata>
          </svg>
        </RouterLink>
        <div
          class="pr-4 cursor-pointer xl:!hidden"
          @click="sidebarShow = false"
        >
          <Icon icon="mdi-close" class="text-2xl" />
        </div>
      </div>
      <div
        v-for="(item, index) of blockchain.computedChainMenu"
        :key="index"
        class="px-2"
      >
        <div
          v-if="isNavGroup(item)"
          :tabindex="index"
          class="collapse"
          :class="{
            'collapse-arrow':index > 0 && item?.children?.length > 0,
            'collapse-open': index === 0 && sidebarOpen,
            'collapse-close': index === 0 && !sidebarOpen,
          }"
        >
          <input
            v-if="index > 0"
            type="checkbox"
            class="cursor-pointer !h-10 block"
            @click="changeOpen(index)"
          />
          <div
            class="collapse-title !py-0 px-4 flex items-center cursor-pointer hover:bg-gray-100 dark:hover:bg-[#373f59]"
          >
            <Icon
              v-if="item?.icon?.icon"
              :icon="item?.icon?.icon"
              class="text-xl mr-2"
              :class="{
                'text-yellow-500': item?.title === 'Favorite',
                'text-blue-500': item?.title !== 'Favorite',
              }"
            />
            <img
              v-if="item?.icon?.image"
              :src="item?.icon?.image"
              class="w-6 h-6 rounded-full mr-3"
            />
            <div
              class="text-base capitalize flex-1 text-gray-700 dark:text-gray-200 whitespace-nowrap"
            >
              {{ item?.title }}
            </div>
            <div
              v-if="item?.badgeContent"
              class="mr-6 badge badge-sm text-white border-none"
              :class="item?.badgeClass"
            >
              {{ item?.badgeContent }}
            </div>
          </div>
          <div class="collapse-content">            
            <div v-for="(el, key) of item?.children" class="menu bg-base-100 w-full !p-0">
              <RouterLink
                v-if="isNavLink(el)"
                @click="sidebarShow = false"
                class="hover:bg-gray-100 dark:hover:bg-[#373f59] rounded cursor-pointer px-3 py-2 flex items-center"
                :class="{
                  '!bg-primary': selected($route, el),
                }"
                :to="el.to"
              >
                <Icon
                  v-if="!el?.icon?.image"
                  icon="mdi:chevron-right"
                  class="mr-2 ml-3"
                  :class="{
                    'text-white':
                      $route.path === el?.to?.path &&
                      item?.title !== 'Favorite',
                  }"
                />
                <img
                  v-if="el?.icon?.image"
                  :src="el?.icon?.image"
                  class="w-6 h-6 rounded-full mr-3 ml-4 " :class="{
                  'border border-gray-300 bg-white': selected($route, el),
                }"
                />
                <div
                  class="text-base capitalize text-gray-500 dark:text-gray-300"
                  :class="{
                    '!text-white': selected($route, el),
                  }"
                >
                  {{ item?.title === 'Favorite' ? el?.title : $t(el?.title) }}
                </div>
              </RouterLink>
            </div>
            <div
              v-if="
                index === 0 && dashboard.networkType === NetworkType.Testnet
              "
              class="menu bg-base-100 w-full !p-0"
            >
              <RouterLink
                class="hover:bg-gray-100 dark:hover:bg-[#373f59] rounded cursor-pointer px-3 py-2 flex items-center"
                :to="`/${blockchain.chainName}/faucet`"
              >
                <Icon icon="mdi:chevron-right" class="mr-2 ml-3"></Icon>
                <div
                  class="text-base capitalize text-gray-500 dark:text-gray-300"
                >
                  Faucet
                </div>
                <div
                  class="badge badge-sm text-white border-none badge-error ml-auto"
                >
                  New
                </div>
              </RouterLink>
            </div>
          </div>
        </div>

        <RouterLink
          v-if="isNavLink(item)"
          :to="item?.to"
          @click="sidebarShow = false"
          class="cursor-pointer rounded-lg px-4 flex items-center py-2 hover:bg-gray-100 dark:hover:bg-[#373f59]"
        >
          <Icon
            v-if="item?.icon?.icon"
            :icon="item?.icon?.icon"
            class="text-xl mr-2"
            :class="{
              'text-yellow-500': item?.title === 'Favorite',
              'text-blue-500': item?.title !== 'Favorite',
            }"
          />
          <img
            v-if="item?.icon?.image"
            :src="item?.icon?.image"
            class="w-6 h-6 rounded-full mr-3 border border-blue-100"
          />
          <div
            class="text-base capitalize flex-1 text-gray-700 dark:text-gray-200 whitespace-nowrap"
          >
            {{ item?.title }}
          </div>
          <div
            v-if="item?.badgeContent"
            class="badge badge-sm text-white border-none"
            :class="item?.badgeClass"
          >
            {{ item?.badgeContent }}
          </div>
        </RouterLink>
        <div
          v-if="isNavTitle(item)"
          class="px-4 text-sm text-gray-400 pb-2 uppercase"
        >
          {{ item?.heading }}
        </div>
      </div>
      <div class="px-2">
        <div class="px-4 text-sm pt-2 text-gray-400 pb-2 uppercase">Tools</div>
        <RouterLink
          to="/wallet/suggest"
          class="py-2 px-4 flex items-center cursor-pointer rounded-lg hover:bg-gray-100 dark:hover:bg-[#373f59]"
        >
          <Icon icon="mdi:frequently-asked-questions" class="text-xl mr-2" />
          <div
            class="text-base capitalize flex-1 text-gray-600 dark:text-gray-200"
          >
            Wallet Helper
          </div>
        </RouterLink>
        <!-- Commenting out Sponsors -->
        <!-- <div class="px-4 text-sm pt-2 text-gray-400 pb-2 uppercase">
          {{ $t('module.sponsors') }}
        </div> -->
        <!-- <Sponsors /> -->
        <div class="px-4 text-sm pt-2 text-gray-400 pb-2 uppercase">
          {{ $t('module.links') }}
        </div>
        <a
          href="https://twitter.com/NeoBase_Studios"
          target="_blank"
          class="py-2 px-4 flex items-center cursor-pointer rounded-lg hover:bg-gray-100 dark:hover:bg-[#373f59]"
        >
          <Icon icon="mdi:twitter" class="text-xl mr-2" />
          <div
            class="text-base capitalize flex-1 text-gray-600 dark:text-gray-200"
          >
            Twitter
          </div>
        </a>
        <!-- <a
          v-if="showDiscord"
          href="https://discord.com/invite/CmjYVSr6GW"
          target="_blank"
          class="py-2 px-4 flex items-center rounded-lg cursor-pointer hover:bg-gray-100 dark:hover:bg-[#373f59]"
        >
          <Icon icon="mdi:discord" class="text-xl mr-2" />
          <div
            class="text-base capitalize flex-1 text-gray-600 dark:text-gray-200"
          >
            Discord
          </div>
        </a> -->
        <a
          href="https://github.com/ping-pub/explorer/discussions"
          target="_blank"
          class="py-2 px-4 flex items-center rounded-lg cursor-pointer hover:bg-gray-100 dark:hover:bg-[#373f59]"
        >
          <Icon icon="mdi:frequently-asked-questions" class="text-xl mr-2" />
          <div
            class="text-base capitalize flex-1 text-gray-600 dark:text-gray-200"
          >
            FAQ
          </div>
        </a>
      </div>
    </div>
    <div class="xl:!ml-64 px-3 pt-4">
      <!-- header -->
      <div
        class="flex items-center py-3 bg-base-100 mb-4 rounded px-4 sticky top-0 z-10"
      >
        <div
          class="text-2xl pr-3 cursor-pointer xl:!hidden"
          @click="sidebarShow = true"
        >
          <Icon icon="mdi-menu" />
        </div>

        <ChainProfile />

        <div class="flex-1 w-0"></div>

        <!-- <NavSearchBar />-->
        <NavBarI18n class="hidden md:!inline-block" />
        <NavbarThemeSwitcher class="!inline-block" />
        <NavbarSearch class="!inline-block" />
        <NavBarWallet />
      </div>

      <!-- 👉 Pages -->
      <div style="min-height: calc(100vh - 180px)">
        <div v-if="behind" class="alert alert-error mb-4">
          <div class="flex gap-2">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              class="stroke-current flex-shrink-0 w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
              ></path>
            </svg>
            <span
              >{{ $t('pages.out_of_sync') }} {{ blocktime.format() }} ({{
                blocktime.fromNow()
              }})</span
            >
          </div>
        </div>
        <RouterView v-slot="{ Component }">
          <Transition mode="out-in">
            <Component :is="Component" />
          </Transition>
        </RouterView>
      </div>

      <newFooter />
    </div>
  </div>
</template>
