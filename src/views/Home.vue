<script lang="tsx">
import { defineComponent, h, ref} from 'vue';
import { LogoWechatStrokeIcon } from 'tdesign-icons-vue-next';

function onClickWechatIcon()
{
    console.log(`click wechat !`)
}

interface CellData
{
    chatId: string,
    title: string,
    description?: string,
    note: string,
    time: number
}

export default defineComponent({
    name: 'HomeView',
    setup() {
        const list = ref<CellData[]>([
            {
                chatId: 'a',
                title: 'chatTitle1',
                description: 'chatDescript1',
                note: 'note1',
                time: 0
            }
        ])

        setTimeout(()=>{
            console.log(`title change!`)
            list.value = [
            {
                chatId: 'b',
                title: 'chatTitle3',
                description: 'chatDescript3',
                note: 'note3',
                time: 0
            },
            ]
        }, 3000)

        const logoWechatStrokeIcon = () => h(LogoWechatStrokeIcon, {size:'2em', onClick: onClickWechatIcon})
        return () => (
          <div class="form">
                <div class='form-item icon-test'>
                    <div style="width:40%">
                        <span>直接引用点击：</span><t-icon name="logo-wechat-stroke" size="2em" onClick={onClickWechatIcon} />
                    </div>
                    <div style="width:40%">
                        <span>render 点击：</span>{ logoWechatStrokeIcon() }
                    </div>
                </div>
                <div class='form-item swipecell-test'>
                    {/* <t-list> */}
                    <div>
                        {
                            list.value.map((one)=>{
                            return (
                                <t-swipe-cell key={one.chatId} v-slots={{
                                    right: () => (
                                        <div class="btn delete-btn">删除</div>
                                    )
                                }}>
                                    <t-cell style="--td-cell-note-font-size: 13;" title={one.title} note={one.note} description={one.description} v-slots={{
                                        leftIcon: () => {
                                            return (<t-avatar shape="circle" image="https://tdesign.gtimg.com/miniprogram/images/example1.png" />)
                                        }
                                    }}/>
                                </t-swipe-cell>
                            )
                        })}
                    </div>
                    {/* </t-list> */}
                </div>
          </div>    
        )
    }
})

</script>
<style scoped land="less">
@import '@/assets/stuffs';
.form
{
    margin: auto;
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    overflow: auto;
}

.form-item
{
    margin-bottom: 10px;
    border-radius: 12px;
    padding: 15px;
    width: 90%;
    background: #ffffffe8;
    box-shadow: 2px 2px 4px 2px rgba(0, 0, 0, 0.10);
}

.icon-test
{
    display: flex;
    justify-content: space-around;
    height: 100px;
}

.swipecell-test
{
    height: 400px;
}

</style>
