<script setup vapor lang="ts">
import liff from '@line/liff'
import { onMounted } from 'vue';

const grandPaImageUrl = 'https://firebasestorage.googleapis.com/v0/b/grandpa-funeral-invitation.firebasestorage.app/o/IMG_1519.JPG?alt=media&token=be64224a-9306-49e8-baae-69462c2eff69'

onMounted(async () => {
  await liff.init({ liffId: import.meta.env.VITE_LIFF_ID });
  if (!liff.isLoggedIn()) {
    if (process.env.NODE_ENV === 'production') {
      liff.login()
    } else {
      liff.login({ redirectUri: window.origin })
    }
  }
})

function onSendShare() {
  liff.shareTargetPicker([
    {
      type: 'flex',
      altText: 'ขอเชิญร่วมรับฟังสวดพระอภิธรรมศพ คุณพ่อ ย้อย แจ้งในเมือง',
      // eslint-disable-next-line @typescript-eslint/ban-ts-comment
      //@ts-ignore
      size: 'giga',
      contents: {
        type: 'bubble',
        hero: {
          type: 'image',
          url: grandPaImageUrl,
          size: 'full',
          aspectRatio: '9:16',
          aspectMode: 'cover',
          action: {
            type: 'uri',
            label: 'Action',
            uri: 'https://linecorp.com/'
          }
        },
        body: {
          type: 'box',
          layout: 'vertical',
          spacing: 'md',
          contents: [
            {
              type: 'box',
              layout: 'vertical',
              contents: [
                {
                  type: 'text',
                  text: 'ขอเชิญร่วมรับฟังสวด',
                  size: 'xl',
                  align: 'center',
                  gravity: 'center',
                  weight: 'bold',
                  color: '#FFFFFF',
                  wrap: true
                },
                {
                  type: 'text',
                  text: 'พระอภิธรรมศพ',
                  size: 'xl',
                  align: 'center',
                  gravity: 'center',
                  weight: 'bold',
                  color: '#FFFFFF',
                  wrap: true
                },
                {
                  type: 'text',
                  text: 'คุณพ่อ ย้อย แจ้งในเมือง',
                  margin: 'md',
                  size: 'xl',
                  align: 'center',
                  gravity: 'center',
                  weight: 'bold',
                  color: '#FFFFFF',
                  wrap: true
                }
              ]
            },
            {
              type: 'box',
              layout: 'vertical',
              contents: [
                {
                  type: 'text',
                  text: 'ณ วัดสรรเพชญ',
                  size: 'lg',
                  align: 'center',
                  color: '#FFFFFF',
                  wrap: true
                },
                {
                  type: 'text',
                  text: 'อำเภอสามพราน จังหวัดนครปฐม',
                  size: 'lg',
                  align: 'center',
                  color: '#FFFFFF',
                  wrap: true
                }
              ]
            },
            {
              type: 'separator',
              margin: 'lg'
            },
            {
              type: 'box',
              layout: 'vertical',
              margin: 'lg',
              contents: [
                {
                  type: 'text',
                  text: 'สวดอภิธรรม ตั้งแต่',
                  align: 'center',
                  color: '#FFFFFF',
                  wrap: true
                },
                {
                  type: 'text',
                  text: 'วันที่ 17 กรกฎาคม พ.ศ.2568',
                  margin: 'md',
                  align: 'center',
                  color: '#FFFFFF',
                  wrap: true
                },
                {
                  type: 'text',
                  text: 'ถึงวันอังคารที่ 22 กรกฎาคม พ.ศ.2568',
                  align: 'center',
                  color: '#FFFFFF',
                  wrap: true
                },
                {
                  type: 'text',
                  text: 'เวลา​ 19:00 น. เป็นต้นไป ที่ศาลา 1',
                  align: 'center',
                  color: '#FFFFFF',
                  wrap: true
                }
              ]
            },
            {
              type: 'box',
              layout: 'vertical',
              margin: 'lg',
              contents: [
                {
                  type: 'text',
                  text: 'เก็บร่างคุณแม่ไว้ 100 วัน',
                  align: 'center',
                  color: '#FFFFFF',
                  wrap: true
                },
                {
                  type: 'text',
                  text: 'ณ วันอังคารที่ 22 กรกฎาคม พ.ศ.2568',
                  size: 'md',
                  align: 'center',
                  color: '#FFFFFF',
                  wrap: true
                },
                {
                  type: 'spacer'
                }
              ]
            }
          ]
        },
        footer: {
          type: 'box',
          layout: 'horizontal',
          flex: 1,
          contents: [
            {
              type: 'button',
              action: {
                type: 'uri',
                label: 'Location สถานที่',
                uri: 'https://goo.gl/maps/EPm4CrEqD1t9kLES7'
              },
              color: '#FFFFFF',
              style: 'secondary'
            }
          ]
        },
        styles: {
          body: {
            backgroundColor: '#27292E'
          },
          footer: {
            backgroundColor: '#27292E'
          }
        }
      }
    }
  ])
}
</script>

<template>
  <div id="app" class="bg-primary h-screen">
    <div class="container mx-auto h-full p-4 flex flex-col justify-center items-center text-center">
      <div class="max-w-xs rounded overflow-hidden shadow-lg mb-8">
        <img alt="Grandpa Image" :src="grandPaImageUrl">
      </div>

      <p class="text-2xl text-white mb-4">ขอเชิญร่วมรับฟังสวดพระอภิธรรมศพ</p>
      <p class="text-2xl text-white mb-4">คุณพ่อ ย้อย แจ้งในเมือง</p>

      <p class="text-xl text-white mb-8">ณ วัดสรรเพชญ อำเภอสามพราน จังหวัดนครปฐม</p>

      <button class="border border-white text-white font-bold py-2 px-4 rounded-full mb-4 cursor-pointer"
        @click="onSendShare">
        สร้างบัตรเชิญร่วมงานผ่าน LINE
      </button>
    </div>
  </div>
</template>
