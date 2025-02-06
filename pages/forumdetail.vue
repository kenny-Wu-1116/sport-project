<template>
  <div class="container mt-3">
    <div class="title">
      <NuxtLink :to="getUrl(data.title)">{{ data.title }}</NuxtLink> {{ data.titlename }}
    </div>
    <TableDetails :data="data.selectedTableData" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from "vue";

export default defineComponent({
  setup() {
    const data = ref<{
      selectedTableData: any[];
      title: string;
      titlename: string;
    }>({
      selectedTableData: [],
      title: "",
      titlename: "",
    });

    const updateTableData = (id: string) => {
      let selectedTableData: any[] = [];
      let title = "";
      let titlename = "";

      switch (id) {
        case "nba1":
          title = "NBA";
          titlename = ">>熱門討論區";
          selectedTableData = [
            { player: "張志明", level: "LV.7 新手教練", content: '<img src="https://picsum.photos/300/300"> 最近看了場比賽，覺得勇士還是很強啊，這次肯定會贏！', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", followers: "1756", },
            { player: "張小娴", level: "LV.10 進階球迷", content: '<img src="https://picsum.photos/300/300"> 熱火最近狀況不錯，對上公牛應該會有驚喜，拭目以待！', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "王永民", level: "LV.12 資深球迷", content: '<img src="https://picsum.photos/300/300"> 每次看獨行俠比賽都很激動，尤其是哈登的表現，這場不容錯過！', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "李靜", level: "LV.5 初學者", content: '上場的比賽中，我感覺塞爾提克比76人還要強，今天他們會贏！', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "周志宏", level: "LV.9 高手球迷", content: '<img src="https://picsum.photos/300/300">', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "蔡明娟", level: "LV.15 神人", content: '<img src="https://picsum.photos/300/300"> 看來這場賽事大概會有一個奇蹟，黃蜂一定會逆襲！', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "李國華", level: "LV.11 球迷大師", content: '<img src="https://picsum.photos/300/300"> 火箭的防守強，這場他們能過關，我挺他們！', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "蘇清華", level: "LV.8 比賽專家", content: ' 不太看好魔術隊的表現，火箭今年的狀態很好，應該能夠輕鬆過關', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "江嘉敏", level: "LV.13 資深球迷", content: ' 今天的比賽對公牛來說不容易，熱火應該還是有機會贏，期待精彩對決！', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "黃玉琳", level: "LV.14 常勝軍", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300">這次我覺得賽季最佳防守球員就是哈登，他的表現太強了，對上76人他能發揮！', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "張宇", level: "LV.6 初學者", content: '<img src="https://picsum.photos/300/300"> 試著挑戰一下這場比賽，看看是否能抓到更多的驚喜時刻，快來一起討論！', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "林宜君", level: "LV.9 高手球迷", content: '<img src="https://picsum.photos/300/300"> 比賽真的很有趣，今天看來會有很多高光時刻，熱火有點被低估了！', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
          ];
          break;

        case "nba2":
          title = "NBA";
          titlename = ">>球隊攻防分析";
          selectedTableData = [
            { player: "王大明", level: "LV.10 進階球迷", content: '<img src="https://picsum.photos/300/300"> 金州勇士的防守真的是太強了，無論是防守策略還是單個球員的防守能力，都是無可挑剔！在對抗湖人的比賽中，他們的防守變陣讓詹姆斯無法發揮出應有的水平。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", followers: "3121", },
            { player: "李志強", level: "LV.15 神人", content: ' 這場比賽中，公牛的快攻防守做得相當到位，熱火的突破被完全限制住了。尤其是在第二節，他們針對熱火的內線進行了加強防守，成效顯著。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "張天宇", level: "LV.12 資深球迷", content: '<img src="https://picsum.photos/300/300"> 獨行俠在對波特蘭的比賽中利用了高位擋拆，這樣的進攻方式讓拓荒者的防守幾乎無從下手。尤其是東契奇的球場視野，讓整個進攻更具威脅。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "高明杰", level: "LV.5 初學者", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300">塞爾提克的防守體系在這場比賽中表現得淋漓盡致，特別是塔圖姆和布朗的協防，成功讓76人難以打開局面。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "黃子傑", level: "LV.9 高手球迷", content: ' 金塊的內線防守在這場比賽中暴露出一些漏洞，太陽的艾頓和布克充分利用了這些缺點，成功拉開了比分。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "陳宏達", level: "LV.10 進階球迷", content: '<img src="https://picsum.photos/300/300">', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "劉建國", level: "LV.5 初學者", content: '明尼蘇達的防守系統中，禮加勒的表現相當搶眼，他不僅能夠準確防守對方球員，還能在關鍵時刻做出抄截，這對快艇的進攻造成了很大的困擾。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "周宇翔", level: "LV.15 神人", content: '<img src="https://picsum.photos/300/300"> 休士頓的進攻戰術充滿了創意，無論是中遠距離的投籃還是快攻，他們的進攻套路都給魔術帶來了很大的壓力。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
            { player: "林奕呈", level: "LV.14 常勝軍", content: ' 鳳凰城的防守反擊戰術實在太高效了，尤其是在比賽下半場，他們成功反制了金塊的高強度進攻，扭轉了比賽局勢。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", },
          ];
          break;

        case "nba3":
          title = "NBA";
          titlename = ">>近期勝率對比";
          selectedTableData = [
            { player: "陳小龍", level: "LV.10 進階球迷", content: '<img src="https://picsum.photos/300/300"> 火箭隊近期勝率有顯著提高，特別是在防守端的強化，這使得他們成功壓制了多支強隊的進攻，整體表現穩定提升。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", followers: "3489" },
            { player: "楊建宏", level: "LV.15 神人", content: '<img src="https://picsum.photos/300/300"> 勇士隊的進攻火力逐漸復甦，尤其是在季後賽中，他們的高效三分球讓勝率大幅提升，進一步改變了比賽走向。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "王智勇", level: "LV.18 資深球迷", content: '湖人隊的勝率在近期上升，他們加強了內線防守，成功限制對手的得分，並以強硬的防守策略穩定取得勝利。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "林家宏", level: "LV.12 資深球迷", content: '熱火隊的勝率穩定上升，特別是在防守轉換方面，他們通過快速反擊創造更多得分機會，成功提升勝率。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "黃文翔", level: "LV.20 常勝軍", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300">鹿角隊近期勝率攀升，球員之間的默契配合以及對防守強度的提升，使得他們的勝率顯著上升，特別是在對抗強隊時表現出色。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "張子楠", level: "LV.22 高手球迷", content: '<img src="https://picsum.photos/300/300"> 76人隊的策略逐漸成熟，近期他們成功突破對手防線，這使得他們的勝率持續上升，並對強敵發起挑戰。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "陳偉良", level: "LV.25 球迷大師", content: ' 太陽隊近期勝率上升，布克和保羅的完美配合，帶動了整體進攻，為球隊的勝率提升奠定了基礎。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "李啟辰", level: "LV.5 初學者", content: '<img src="https://picsum.photos/300/300">', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "林家宏", level: "LV.12 資深球迷", content: ' 熱火隊最近的防守表現強勢，尤其在快攻時的反擊速度，讓他們的勝率不斷提升，並在比賽中取得優勢。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "黃文翔", level: "LV.20 常勝軍", content: '<img src="https://picsum.photos/300/300"> 鹿角隊強化防守及球場空間控制的策略，使他們在近期的比賽中連勝，提升了整體的勝率。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
          ];
          break;

        case "nba4":
          title = "NBA";
          titlename = ">>明星球員表現";
          selectedTableData = [
            { player: "李佳穎", level: "LV.7 新手教練", content: '湖人隊的 LeBron James 在近期比賽中展現了出色的領導能力，不僅在進攻端能有效組織戰術，在防守端也帶動隊友積極回防，為球隊穩定提升表現。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", followers: "2948" },
            { player: "陳德華", level: "LV.10 進階球迷", content: '<img src="https://picsum.photos/300/300"> 快艇隊的 Kawhi Leonard 在防守端的表現不可小覷，他在對陣金州勇士的比賽中成功限制了 Stephen Curry，讓對方進攻陷入停滯，這對球隊的防守體系有著極大貢獻。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "王書維", level: "LV.12 資深球迷", content: '太陽隊的 Devin Booker 在近期比賽展現了極高的得分能力，無論是三分球還是中距離跳投，都讓對手防不勝防，他的穩定輸出成為球隊取勝的重要關鍵。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "林國華", level: "LV.5 初學者", content: '<img src="https://picsum.photos/300/300"> 76人隊的 Joel Embiid 近期比賽發揮 MVP 水準，他在禁區的統治力讓對手無法有效得分，同時他的罰球命中率也幫助球隊穩定進攻。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "周志明", level: "LV.9 高手球迷", content: '勇士隊的 Stephen Curry 在比賽中發揮了神射手本色，連續投進多顆關鍵三分球，帶領球隊逆轉比賽，證明了他依舊是聯盟最具威脅性的射手之一。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "張家俊", level: "LV.15 神人", content: '<img src="https://picsum.photos/300/300"> 熱火隊的 Jimmy Butler 在季後賽模式開啟後，展現了超凡的鬥志與決心，他的強硬打法和穩定中距離投籃，讓熱火隊成為東區競爭力最強的球隊之一。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "李政傑", level: "LV.11 球迷大師", content: '<img src="https://picsum.photos/300/300"> 公鹿隊的 Giannis Antetokounmpo 在攻防兩端都展現出統治力，他的快攻突破幾乎無人能擋，加上防守端的封蓋和籃板，幫助球隊取得連勝。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "王書維", level: "LV.5 初學者", content: '<img src="https://picsum.photos/300/300">', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "林國華", level: "LV.13 資深球迷", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300"> 76人隊的 Tyrese Maxey 在近期比賽成長迅速，他的突破與三分投射能力，使球隊在 Embiid 缺陣時仍能保持進攻火力，展現出未來明星的潛力。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "周志明", level: "LV.14 常勝軍", content: ' 太陽隊的 Kevin Durant 利用他的身高與投射能力，在關鍵時刻命中多記中距離跳投，為球隊鎖定勝局，他的經驗與穩定性仍是聯盟頂級球星的象徵。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
          ];
          break;

        case "nba5":
          title = "NBA";
          titlename = ">>最新比賽資訊";
          selectedTableData = [
            { player: "何俊傑", level: "LV.10 進階球迷", content: '<img src="https://picsum.photos/300/300"> 熱火隊的進攻體系在本賽季展現出色的流暢度，尤其是對於快速轉換攻擊的運用，將對方防線拉得四分五裂。高宇哲觀察到熱火隊在快攻時的突破點不斷變化，擁有多種攻擊手段，這使得對手無法有效應對。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", followers: "2948" },
            { player: "陳德華", level: "LV.15 神人", content: '快艇隊在本賽季的防守端表現突出，特別是在防守反擊時，陳德華分析了他們如何利用高強度的全場緊逼來限制對方的傳球選擇，使得對方的進攻節奏頻繁受到干擾。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "王書維", level: "LV.12 資深球迷", content: '<img src="https://picsum.photos/300/300">', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "林國華", level: "LV.9 高手球迷", content: '<img src="https://picsum.photos/300/300"> 76人隊最近的比賽中，他們的防守策略愈發精緻，特別是在對方控球後衛的防守上，林國華分析了76人隊如何針對對方的主力球員進行針對性防守，通過不斷換防和協防來有效限制對方的進攻威脅。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "周志明", level: "LV.8 比賽專家", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300"> 湖人隊在進攻端的配合愈發默契，尤其是在高位擺放的戰術上，周志明指出，湖人隊的進攻不僅依賴於詹姆斯的個人能力，更重要的是他們的空間管理和二人轉換配合，這讓對方防守難以找到有效應對的方案。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "張家俊", level: "LV.11 球迷大師", content: ' 勇士隊的三分球攻勢本賽季依然強大，張家俊指出，勇士隊的戰術設計讓球員間的傳球和掩護配合達到極致，無論是在快攻還是在半場進攻中，他們總能找到最適合的射手來完成進攻。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "李政傑", level: "LV.14 常勝軍", content: '熱火隊的防守策略和進攻節奏，在最近的比賽中取得了顯著的成效。李政傑分析了他們如何運用變化多端的防守方式來混淆對手的進攻路線，並且在反擊中充分利用內外線的配合來發揮進攻威脅。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
          ];
          break;

        case "nba6":
          title = "NBA";
          titlename = ">>專家分析推薦";
          selectedTableData = [
            { player: "周采妮", level: "LV.10 進階球迷", content: '<img src="https://picsum.photos/300/300"> 透過近期比賽分析，我們可以看到隊伍在場上的控球與領導能力，特別是在隊友需要支援時，總能提供關鍵助攻。專家指出，球隊的視野與傳球能力對比賽節奏的掌控有著重要影響，顯示出他們在比賽中扮演著至關重要的角色。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", followers: "3248" },
            { player: "陳國華", level: "LV.15 神人", content: '<img src="https://picsum.photos/300/300"> 隊伍的球風穩定且準確，尤其在比賽的高壓時刻，能夠保持冷靜，並準確完成得分。專家分析了他們如何利用比賽節奏突破防守，並創造更多得分機會，使對方防守球員無法預測他們的下一步動作。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "楊浩然", level: "LV.12 資深球迷", content: '專家指出，球隊作為多面手球員，不僅在防守端表現優異，還能有效消耗對手體力。防守腳步靈活，能夠有效限制對方主力球員的發揮，並為球隊創造有利局面。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "黃志傑", level: "LV.13 資深球迷", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300">球隊的爆發力和精確的投射能力讓他們成為聯盟中最具威脅的得分手之一。專家深入分析了球隊如何運用快速跑位和精准射程來擾亂防守佈局，在比賽關鍵時刻爭取更多進攻機會。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "李俊宏", level: "LV.14 常勝軍", content: '<img src="https://picsum.photos/300/300"> 球隊在比賽中的冷靜態度和智慧，使他們成為對手難以防範的威脅。專家分析了他們如何在關鍵時刻運用場上佈局，並強調了突破防守、精確傳球的能力，使他們能夠在比賽中冷靜應對高壓局面。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "周振宇", level: "LV.9 高手球迷", content: '<img src="https://picsum.photos/300/300">', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "黃子傑", level: "LV.8 比賽專家", content: '專家提到，球隊在無球跑位方面的能力極為高效，總能抓住每一個進攻機會，並利用極快的速度突破對方防線，這使他們成為場上難以防範的存在。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
          ];
          break;

        case "mlb1":
          title = "MLB";
          titlename = " >> 球隊近況解析";
          selectedTableData = [
            { player: "鄭文豪", level: "LV.7 新手教練", content: '<img src="https://picsum.photos/300/300"> 本賽季球隊表現穩定，最近取得了連勝，尤其是在打擊端的表現不錯。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", followers: "4526" },
            { player: "李德明", level: "LV.10 進階球迷", content: ' 球隊近期的防守改進顯著，尤其在與強隊對戰時，他們的防守策略給對手帶來了不少麻煩。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "陳建華", level: "LV.12 資深球迷", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300"> 最近球隊的投手表現優異，特別是新加入的投手，對比賽的影響很大。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "張志明", level: "LV.15 神人", content: '<img src="https://picsum.photos/300/300"> 最近球隊的整體合作默契有了明顯提升，尤其是打擊與投球間的配合更加順暢。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "黃俊傑", level: "LV.9 高手球迷", content: '<img src="https://picsum.photos/300/300"> 球隊的投手表現穩定，尤其是在關鍵局數，總是能夠穩住場面，幫助球隊取得重要勝利。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "吳淑萍", level: "LV.11 球迷大師", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300"> 球隊的整體攻守平衡越來越好，尤其是在大比分落後時，他們的逆襲能力強。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "林怡君", level: "LV.13 資深球迷", content: '球隊的後備球員也有亮眼表現，為球隊提供了更多戰術選擇。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "周家宏", level: "LV.14 常勝軍", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300"> 球隊的防守組織相當緊密，尤其是捕手與投手之間的默契配合，令對手難以得分。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "蔡建宏", level: "LV.8 比賽專家", content: '<img src="https://picsum.photos/300/300"> 球隊近期的發揮越來越穩定，尤其是在重要的比賽中，總能保持高水平的表現。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
          ];
          break;

        case "mlb2":
          title = "MLB";
          titlename = " >> 投手與打者數據";
          selectedTableData = [
            { player: "許佩珊", level: "LV.7 新手教練", content: '<img src="https://picsum.photos/300/300"> 投手表現不錯，最近的控球穩定，對於打者的打擊也有明顯壓制效果。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", followers: "4526" },
            { player: "李志強", level: "LV.10 進階球迷", content: '投手最近的球速有了提升，但還需要在控制球上加強，這樣能更有效地應對強打者。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "劉建華", level: "LV.12 資深球迷", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300"> 打者的擊球率穩定，尤其是與快速球對決時表現出色。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "陳小華", level: "LV.9 高手球迷", content: '<img src="https://picsum.photos/300/300"> 近期打者的心態調整良好，面對不同投手能夠做出更有效的應對。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "張建業", level: "LV.15 神人", content: '<img src="https://picsum.photos/300/300"> 投手的變化球威脅逐漸增大，對打者的影響越來越明顯。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "王俊傑", level: "LV.11 球迷大師", content: '<img src="https://picsum.photos/300/300"> 打者的準確度越來越高，特別是在對右投手的攻擊上，已經逐漸形成了一套獨特的打法。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "劉俊偉", level: "LV.8 比賽專家", content: '面對強投手時，打者的心理素質越來越好，攻擊意識也更強。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "李光豪", level: "LV.13 資深球迷", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300"> 投手最近狀態不錯，但打者需要提高應對變速球的能力。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "陳偉杰", level: "LV.14 常勝軍", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300"> 投手的控球越來越準確，但仍需加強變化球的使用，以提高壓制力。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "王志強", level: "LV.6 初學者", content: '最近的打者有了明顯進步，尤其是在大賽中對關鍵時刻的應對能力強。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "李佳琦", level: "LV.9 高手球迷", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300"> 投手的表現進一步提升，打者也能夠充分發揮壓迫性，對比賽節奏的控制有了更大的掌握。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "張國榮", level: "LV.15 神人", content: '<img src="https://picsum.photos/300/300"> 打者最近的表現非常穩定，尤其是在對較強投手的比賽中，依然能夠保證高水準的打擊。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
          ];
          break;

        case "mlb3":
          title = "MLB";
          titlename = " >> 近期排名與戰績";
          selectedTableData = [
            { player: "楊宗翰", level: "LV.7 新手教練", content: '<img src="https://picsum.photos/300/300"> 最近的排名穩步上升，球隊表現不錯。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", followers: "4526" },
            { player: "林子豪", level: "LV.15 神人", content: '<img src="https://picsum.photos/300/300"> 排名穩定，一直在前幾名之內，近期狀況火熱！', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "楊德華", level: "LV.15 神人", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300"> 近期球隊表現強勁，排在聯盟前五！', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "蔡明哲", level: "LV.14 常勝軍", content: '<img src="https://picsum.photos/300/300"> 球隊的表現越來越好，最近的連勝讓排名逐漸上升。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "陳冠霖", level: "LV.12 資深球迷", content: ' 球隊狀態逐漸回升，排名穩定在前十名內。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "黃俊傑", level: "LV.10 進階球迷", content: '<img src="https://picsum.photos/300/300"> 球隊實力強大，最近的連勝讓排名迅速上升。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "李昕儀", level: "LV.11 球迷大師", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300"> 排名穩定，近期戰績優異，球隊實力不容小覷。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "劉家豪", level: "LV.9 高手球迷", content: ' 球隊目前排名不錯，期待接下來的比賽能夠繼續上升。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "陳立威", level: "LV.8 比賽專家", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300"> 球隊表現不錯，排名逐漸上升，整體狀況佳。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "黃志偉", level: "LV.13 資深球迷", content: '球隊的表現令人驚艷，近期排名穩步上升，戰績亮眼。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
          ];
          break;

        case "mlb4":
          title = "MLB";
          titlename = " >> 大數據勝率分析";
          selectedTableData = [
            { player: "林美玲", level: "LV.7 新手教練", content: '<img src="https://picsum.photos/300/300"> 最近的數據分析顯示，這支球隊的勝率穩定提升。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", followers: "4526" },
            { player: "李大維", level: "LV.15 神人", content: '<img src="https://picsum.photos/300/300"> 球隊數據表現突出，勝率逐月上升。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "張家豪", level: "LV.12 資深球迷", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300"> 根據大數據分析，這支球隊最近狀況火熱，表現穩定。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "王家興", level: "LV.9 高手球迷", content: ' 球隊的勝率指數近期上升，數據顯示穩步增長。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "李佩蓉", level: "LV.15 神人", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300"> 最近的比賽讓球隊的勝率穩步上升。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "王志明", level: "LV.14 常勝軍", content: '<img src="https://picsum.photos/300/300"> 大數據分析顯示，球隊整體表現非常強勁。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "陳韋君", level: "LV.13 資深球迷", content: '球隊的數據表現強勁，預計將持續保持高勝率。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "李昕儀", level: "LV.11 球迷大師", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300"> 勝率持續攀升，數據顯示球隊狀態非常穩定。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "張致遠", level: "LV.10 進階球迷", content: '<img src="https://picsum.photos/300/300"> 球隊的勝率分析顯示，長期的表現相當穩定。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
          ];
          break;

        case "mlb5":
          title = "MLB";
          titlename = " >> 球員表現分析";
          selectedTableData = [
            { player: "陳志明", level: "LV.7 新手教練", content: '<img src="https://picsum.photos/300/300">這位球員在最近的比賽中表現穩定，提供了關鍵助攻。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300", followers: "4526" },
            { player: "李大維", level: "LV.15 神人", content: '最近的得分能力驚人，尤其在關鍵時刻的表現無可挑剔。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "張家豪", level: "LV.14 常勝軍", content: '<img src="https://picsum.photos/300/300">防守堅強，這位球員在最近的比賽中幾次阻止對手進攻。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "王家興", level: "LV.13 資深球迷", content: '在比賽中展現了強大的爆發力，迅速改變了比賽局勢。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "李佩蓉", level: "LV.12 資深球迷", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300">她的連續得分為球隊注入了活力，成為關鍵球員。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "王志明", level: "LV.10 進階球迷", content: '<img src="https://picsum.photos/300/300">近期表現穩定，防守端無懈可擊，幾乎無法突破。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "陳韋君", level: "LV.9 高手球迷", content: '<img src="https://picsum.photos/300/300">這位球員的速度讓對手難以防範，迅速進攻並取得分數。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "李昕儀", level: "LV.8 比賽專家", content: '<img src="https://picsum.photos/300/300"> <img src="https://picsum.photos/300/300">在上場比賽中，她的關鍵表現幫助球隊贏得勝利。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
            { player: "張致遠", level: "LV.11 球迷大師", content: '其穩定的表現和冷靜的頭腦，為球隊貢獻了不小的分數。', date: "2024-03-25 19:06:17", image: "https://picsum.photos/300/300" },
          ];
          break;

        default:
          selectedTableData = [];
      }

      return { selectedTableData, title, titlename };
    };

    const getUrl = (title: string) => {
      switch (title) {
        case "NBA":
          return "/forum";
        case "MLB":
          return "/forum";
        default:
          return "#";
      }
    };

    onMounted(() => {
      const params = new URLSearchParams(window.location.search);
      const id = params.get("id");
      if (id) {
        data.value = updateTableData(id);
      }
    });

    return {
      data,
      getUrl,
    };
  },
});
</script>

<style scoped>
.container {
  max-width: 1000px;
}

.title {
  color: rgb(94, 94, 94);
  font-size: 18px;
  font-weight: bold;
  padding: 8px;
}

.title a {
  color: rgb(33, 89, 168);
  text-decoration: none;
}

.title a:hover {
  color: blue;
  text-decoration: underline;
}
</style>