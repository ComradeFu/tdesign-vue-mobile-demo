<script lang="tsx">
import { defineComponent, h, ref} from 'vue';
import { LogoWechatStrokeIcon } from 'tdesign-icons-vue-next';

function onClickWechatIcon()
{
    console.log(`click wechat !`)
}

interface CellData
{
    chatId: number,
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
                chatId: 1,
                title: 'chatTitle1',
                description: 'chatDescript1',
                note: 'note1',
                time: 0
            },
            {
                chatId: 2,
                title: 'chatTitle2',
                description: 'chatDescript22222',
                note: 'note2',
                time: 0
            },
            {
                chatId: 3,
                title: 'chatTitle3',
                description: 'chatDescript33333',
                note: 'note1',
                time: 0
            },
            {
                chatId: 4,
                title: 'chatTitle4',
                description: 'chatDescript4444',
                note: 'note1',
                time: 0
            },
            {
                chatId: 5,
                title: 'chatTitle5',
                description: 'chatDescript55555',
                note: 'note1',
                time: 0
            }
        ])

        setTimeout(()=>{
            console.log(`title change!`)
            list.value.sort((a, b) => b.chatId - a.chatId)
            
        }, 3000)

        const logoWechatStrokeIcon = () => h(LogoWechatStrokeIcon, {size:'2em', onClick: onClickWechatIcon})

        let selectState = ref({
          show: false,
          selected: '',
        });

        function onPick(value: string[]) {
          console.log(`picker pick`)
          console.log(value)
        }

        const areaOptions = [[{
                label: "a",
                value: "a"
            },
            {
                label: "b",
                value: "b"
            }
        ]]

        const pickValue = ref([])

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
                <t-pull-down-refresh class='form-item' onRefresh={()=>console.log(`pull down refresh.`)}>
                    <t-list class="swipecell-test">
                        {
                            list.value.map((one, index)=>{
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
                    </t-list>
                </t-pull-down-refresh>
                <div class="form-item t-picker-test">
                    <t-cell
                        arrow
                        title="选择地区"
                        note={selectState.value.selected}
                        onClick={() => {
                            console.log(`click cell!!!`);
                            selectState.value.show = true;
                        }}
                        />
                        <t-popup v-model={selectState.value.show} placement="bottom">
                            <t-picker
                                v-model={pickValue.value}
                                columns={areaOptions}
                                onConfirm={() => {
                                    selectState.value.show = false;
                                }}
                                onCancel={() => {
                                    selectState.value.show = false;
                                }}
                                pick={onPick}
                            />
                        </t-popup>
                </div>
                <div class="form-item t-picker-test2">
                    <t-cell
                        arrow
                        title="选择地区2"
                        note={selectState.value.selected}
                        onClick={() => {
                            console.log(`click cell!!!`);
                            selectState.value.show = true;
                        }}
                        />
                        <t-popup v-model={selectState.value.show} placement="bottom">
                            <t-picker
                                v-model={pickValue.value}
                                columns={areaOptions}
                                onConfirm={(data: any) => {
                                    console.log(`click confirm!!!`)
                                    console.log(data)
                                    selectState.value.show = false;
                                }}
                                onCancel={() => {
                                    selectState.value.show = false;
                                }}
                                pick={onPick}
                            />
                        </t-popup>
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
    height: 300px;
    overflow: auto;
}

</style>
