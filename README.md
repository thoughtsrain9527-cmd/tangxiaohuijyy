
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
  <meta name="theme-color" content="#ff6b8b">
  <title>浪漫表白 - 汤晓慧专属</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Font Awesome -->
  <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
  <!-- GSAP 动画库 -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
  
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            primary: '#ff6b8b',
            secondary: '#ff8fa3',
            accent: '#ffc2d1',
            dark: '#e63946',
            light: '#fff1f2'
          },
          fontFamily: {
            sans: ['Arial', 'sans-serif'],
            display: ['Comic Sans MS', 'cursive']
          },
          animation: {
            'pulse-slow': 'pulse 3s cubic-bezier(0.4, 0, 0.6, 1) infinite',
            'float': 'float 3s ease-in-out infinite',
            'glow': 'glow 2s ease-in-out infinite alternate'
          },
          keyframes: {
            float: {
              '0%, 100%': { transform: 'translateY(0)' },
              '50%': { transform: 'translateY(-10px)' }
            },
            glow: {
              '0%': { textShadow: '0 0 5px #fff, 0 0 10px #fff, 0 0 15px #ff6b8b, 0 0 20px #ff6b8b' },
              '100%': { textShadow: '0 0 10px #fff, 0 0 20px #fff, 0 0 30px #ff6b8b, 0 0 40px #ff6b8b' }
            }
          }
        }
      }
    }
  </script>
  
  <style type="text/tailwindcss">
    @layer utilities {
      .text-shadow {
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
      }
      .text-shadow-glow {
        text-shadow: 0 0 5px #fff, 0 0 10px #fff, 0 0 15px #ff6b8b, 0 0 20px #ff6b8b;
      }
      .btn-heart {
        transition: all 0.3s ease;
        touch-action: manipulation;
        -webkit-tap-highlight-color: transparent;
      }
      .btn-heart:hover, .btn-heart:focus {
        transform: scale(1.1);
        filter: brightness(1.2);
        outline: none;
      }
      .btn-heart:active {
        transform: scale(0.95);
      }
      .btn-heart:active::after {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(255, 255, 255, 0.3);
        border-radius: 50%;
        animation: ripple 0.6s ease-out;
      }
      @keyframes ripple {
        0% {
          transform: scale(0.8);
          opacity: 1;
        }
        100% {
          transform: scale(2.5);
          opacity: 0;
        }
      }
      .audio-control {
        touch-action: manipulation;
        -webkit-tap-highlight-color: transparent;
      }
      .loader {
        border: 4px solid rgba(255, 255, 255, 0.3);
        border-radius: 50%;
        border-top: 4px solid #ff6b8b;
        width: 40px;
        height: 40px;
        animation: spin 1s linear infinite;
      }
      @keyframes spin {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
      }
      .share-btn {
        touch-action: manipulation;
        -webkit-tap-highlight-color: transparent;
      }
      .heart {
        position: absolute;
        pointer-events: none;
        animation: float 3s ease-in-out infinite;
      }
      .hand-heart {
        position: absolute;
        pointer-events: none;
        font-size: 36px;
        color: #ff6b8b;
        opacity: 0;
        text-shadow: 0 0 10px rgba(255, 107, 139, 0.8);
      }
      .romantic-text {
        position: absolute;
        color: white;
        font-weight: bold;
        font-family: 'Comic Sans MS', cursive;
        opacity: 0;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
      }
      .final-text-container {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        text-align: center;
        z-index: 10;
        opacity: 0;
        transition: opacity 1s ease-in-out;
      }
      .particle {
        position: absolute;
        pointer-events: none;
        border-radius: 50%;
        background-color: rgba(255, 255, 255, 0.8);
        box-shadow: 0 0 10px rgba(255, 255, 255, 0.8);
        animation: float 3s ease-in-out infinite;
      }
      .audio-control {
        position: absolute;
        bottom: 15px;
        right: 15px;
        z-index: 20;
        cursor: pointer;
        width: 40px;
        height: 40px;
        border-radius: 50%;
        background-color: rgba(255, 255, 255, 0.8);
        display: flex;
        justify-content: center;
        align-items: center;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
        transition: all 0.3s ease;
      }
      .audio-control:hover {
        transform: scale(1.1);
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
      }
      .audio-icon {
        font-size: 20px;
        color: #ff6b8b;
      }
      .final-text {
        font-family: 'Comic Sans MS', cursive;
        color: white;
        text-shadow: 0 0 15px #fff, 0 0 30px #fff, 0 0 45px #ff6b8b, 0 0 60px #ff6b8b;
        animation: glow 1.5s ease-in-out infinite alternate;
      }
      #canvas-container {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        pointer-events: none;
        z-index: 5;
      }
      #fireworks-canvas {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
      }
      #hearts-canvas {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
      }
      .cover {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(255, 241, 242, 0.9);
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        z-index: 20;
        transition: opacity 1s ease-out;
      }
      .cover.hidden {
        opacity: 0;
        pointer-events: none;
      }
      /* 9:16容器样式 */
      .phone-container {
        position: relative;
        width: 100%;
        max-width: 420px;
        margin: 0 auto;
        overflow: hidden;
      }
      .phone-container::before {
        content: '';
        display: block;
        padding-top: 177.78%; /* 9:16比例 (16/9 = 1.777...) */
      }
      .phone-content {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        overflow: hidden;
      }
    }
  </style>
</head>
<body class="bg-gray-100 flex items-center justify-center min-h-screen p-4">
  <!-- 加载动画 -->
  <div id="loader" class="fixed inset-0 flex items-center justify-center bg-light z-50">
    <div class="text-center">
      <div class="loader mx-auto mb-4"></div>
      <p class="text-primary font-display text-lg">加载中...</p>
    </div>
  </div>
  
  <!-- 9:16手机容器 -->
  <div class="phone-container">
    <div class="phone-content bg-light overflow-hidden">
      <!-- 封面页 -->
      <div class="cover" id="cover">
        <div class="absolute inset-0 bg-cover bg-center opacity-30" style="background-image: url('https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/fdb6dbce249744239699a0471a05a51c~tplv-a9rns2rl98-image.image?rcl=202511111315231FB26BDAA64FAA02B47D&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1765430146&x-signature=qFU9AmbgIEJ78o%2BQnLTa%2Fh0jPMY%3D')"></div>
        <div class="relative text-center mb-8">
          <h2 class="text-2xl font-display font-bold text-secondary mb-2 animate-float">汤晓慧专属</h2>
          <h1 class="text-4xl font-display font-bold text-primary mb-4 animate-float text-shadow-glow">乖乖点击</h1>
          <p class="text-lg text-gray-600">点击下方爱心，开启浪漫之旅</p>
        </div>
        <button id="heart-btn" class="btn-heart cursor-pointer animate-pulse-slow">
          <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/1103d3de758d4f9395322bda3b03338a~tplv-a9rns2rl98-image.image?rcl=202511111222158343F5A91910809ECDA4&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1765426971&x-signature=3QR9k1OOIqxYRr70kn5owjmuwrI%3D" 
               alt="全新设计的粉色爱心按钮" 
               class="w-28 h-28 object-contain">
        </button>
      </div>
      
      <!-- 音频控制 -->
      <div class="audio-control" id="audio-control">
        <i class="fa fa-music audio-icon" id="audio-icon"></i>
      </div>
      
      <!-- 分享按钮 -->
      <div id="share-btn" class="fixed bottom-15 left-15 z-20 cursor-pointer w-10 h-10 rounded-full bg-white bg-opacity-80 flex justify-center items-center shadow-md transition-all duration-300 share-btn">
        <i class="fa fa-share-alt text-primary text-xl"></i>
      </div>
      
      <!-- 分享提示 -->
      <div id="share-toast" class="fixed bottom-24 left-1/2 transform -translate-x-1/2 bg-gray-800 text-white px-4 py-2 rounded-lg shadow-lg opacity-0 transition-opacity duration-300 z-20">
        点击右上角分享给TA
      </div>
      
      <!-- 音频元素 -->
      <audio id="background-music" loop>
        <source src="https://file.1115111.xyz/2024/07/17/12yug1t.m4a" type="audio/mpeg">
      </audio>

      <!-- 背景容器 -->
      <div class="absolute inset-0 bg-cover bg-center z-0" style="background-image: url('https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/fdb6dbce249744239699a0471a05a51c~tplv-a9rns2rl98-image.image?rcl=202511111315231FB26BDAA64FAA02B47D&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1765430146&x-signature=qFU9AmbgIEJ78o%2BQnLTa%2Fh0jPMY%3D')"></div>
      
      <!-- 粒子背景 -->
      <div id="particles-container" class="absolute inset-0 z-1 pointer-events-none"></div>

      <!-- Canvas 容器 -->
      <div id="canvas-container">
        <canvas id="hearts-canvas"></canvas>
        <canvas id="fireworks-canvas"></canvas>
      </div>

      <!-- 浪漫文字容器 -->
      <div id="romantic-text-container"></div>
      
      <!-- 比心动画容器 -->
      <div id="hand-hearts-container"></div>

      <!-- 最终表白文案 -->
      <div class="final-text-container" id="final-text-container">
        <div class="relative p-6 rounded-2xl bg-white bg-opacity-20 backdrop-blur-sm border border-pink-200 shadow-lg">
          <h2 class="final-text text-3xl mb-2">汤晓慧</h2>
          <p class="final-text text-3xl mb-3">我爱你</p>
          <p class="final-text text-xl">永远爱你的蒋永雨</p>
        </div>
      </div>
    </div>
  </div>
  


  <script>
    // 等待DOM加载完成
    document.addEventListener('DOMContentLoaded', function() {
      // 获取DOM元素
      const cover = document.getElementById('cover');
      const heartBtn = document.getElementById('heart-btn');
      const romanticTextContainer = document.getElementById('romantic-text-container');
      const handHeartsContainer = document.getElementById('hand-hearts-container');
      const finalTextContainer = document.getElementById('final-text-container');
      const heartPath = document.getElementById('heart-path');
      const heartsCanvas = document.getElementById('hearts-canvas');
      const fireworksCanvas = document.getElementById('fireworks-canvas');
      const particlesContainer = document.getElementById('particles-container');
      const audioControl = document.getElementById('audio-control');
      const audioIcon = document.getElementById('audio-icon');
      const backgroundMusic = document.getElementById('background-music');
      
      // 设置Canvas尺寸
      function resizeCanvas() {
        const phoneContent = document.querySelector('.phone-content');
        const width = phoneContent.offsetWidth;
        const height = phoneContent.offsetHeight;
        
        heartsCanvas.width = width;
        heartsCanvas.height = height;
        fireworksCanvas.width = width;
        fireworksCanvas.height = height;
      }
      
      resizeCanvas();
      window.addEventListener('resize', resizeCanvas);
      
      // 获取Canvas上下文
      const heartsCtx = heartsCanvas.getContext('2d');
      const fireworksCtx = fireworksCanvas.getContext('2d');
      
      // 甜蜜昵称数组（520个）
      const romanticTexts = [
        '宝贝', '亲爱的', '老公', '老婆', '达令', '乖乖', '傻瓜', '笨蛋', '小可爱', '小甜心',
        '小心肝', '心肝宝贝', '哥哥', '妹妹', '姐姐', '弟弟', '先生', '太太', '我的爱', '小傻瓜',
        '我的小祖宗', '小朋友', '小猪', '小猪猪', '小熊', '小狗', '修勾', '小猫', '喵喵', '小兔子',
        '小鹿', '小狐狸', '小企鹅', '小仓鼠', '小青蛙', '皮卡丘', '大狗狗', '考拉', '小糖果', '糖糖',
        '小蛋糕', '小布丁', '小饼干', '小蛋挞', '小奶包', '小泡芙', '小草莓', '小苹果', '小汤圆', '小糯米',
        '小甜甜圈', '蜂蜜', '芝士', '奶茶宝宝', '彬彬', '小静', '呆子', '懒虫', '猪猪侠', '老板',
        '领导', '管家婆', '管家公', '大聪明', '小笨蛋', '小迷糊', '小哭包', '爱哭鬼', '小醋精', '醋王',
        '小太阳', '小超人', '我的树洞', '小话痨', '我的开心果', '小粘人精', '宝批龙', '憨憨', '铁憨憨', '哈宝',
        '哈儿', '小废物', '我的ATM', '饭搭子', '干饭搭子', '游戏搭子', '饲养员', '小祖宗', '祖宗大人', '冤种',
        '老六', '赔钱货', '瓜娃子', '靓仔', '靓女', '狗子', '我的世界', '我的心跳', '我的呼吸', '我的光',
        '我的海', '我的港湾', '小宇宙', '小行星', '另一半', '灵魂伴侣', '此生挚爱', '良人', '小确幸', '唯一',
        'Honey', '哈尼', 'Darling', 'Sweetheart', 'Sweetie', 'Baby', 'Mon Chéri', 'Ma Chérie', '朝朝', '暮暮',
        '山止', '川行', '奶糖', '布丁', '星轨', '月轨', '雾散', '风起', '桃枝', '梨雪',
        '左耳', '右耳', '软糖', '硬糖', '白粥', '小菜', '晴日', '阴天', '汽水', '冰块',
        '南巷', '北里', '早睡', '晚起', '书齐', '页合', '茶白', '酒红', '桃酥', '杏脯',
        '灯明', '火暖', '鲸落', '星沉', '左顾', '右盼', '春衫', '冬袄', '折枝', '赠春',
        '关雎', '鹿鸣', '闻卿至', '待君归', '星河揽月客', '清风伴花影', '松下听琴者', '竹间抚瑟人', '枕星河入梦', '拥朝雾而眠',
        '南巷暖阳', '北岛繁星', '星眸藏梦夜', '樱唇启笑晨', '白茶相依', '柚茶暖心', '雨落听风', '花开恋蝶', '迷途寻光者', '错位识途星',
        '岁暮', '南山', '南风过境', '梦至西洲', '八千里海岸', '七厘米蔚蓝', '日落放映机', '日落放映员', '迟早', '迟早是我的',
        '听我碎碎念', '陪我岁岁年', '山野雾', '海岛风', '云欲从月', '花遇和风', '似朝朝', '亦暮暮', '眼里有星河', '星河皆是你',
        '将心予明月', '明月再付卿', '晚风', '偏爱晚风', '与你同行', '不介路远', '南有溪川', '北冥有鱼', '朝朝念你', '暮暮想你',
        '月亮轻颤', '像我看见你的悸动', '银河间', '躲在银河间', '贩卖月光', '收藏温柔', '落日放映', '心动影片', '星沉月落', '你入我梦',
        '枕边情书', '梦里情话', '长街听风', '短巷吻雨', '清风绕指柔', '暖阳映心暖', '白茶清欢无别事', '我在等风也等你', '萌兔跳跳', '憨熊抱抱',
        '奶糖味的小仙女', '巧克力味的小王子', '小熊软糖', '小兔奶糖', '甜心宝贝', '宠妻狂魔', '萌面大侠', '傻气小侠', '嘟嘟熊', '泡泡兔',
        '小懒猫', '大暖狗', '糖宝', '蜜宝', '呆呆萌', '傻傻爱', '萌宝驾到', '宠宝跟上', '墨染幽篁', '诗韵兰舟',
        '清风舞明月', '幽梦绕佳人', '浅酌桃花酒', '慢品杏花茶', '素笺墨韵', '红袖添香', '南乔枝', '北归雁', '琴瑟和鸣', '钟鼓乐之',
        '画扇轻摇花落去', '珠帘半卷月归来', '青衫隐', '红袖藏', '桃之夭夭', '灼灼其华', '执笔画卿颜', '倚楼听君语', '森屿暖树', '墒以光年',
        '浅梦流年', '静语时光', '薄荷微光少年时', '柠檬初语少女心', '晨曦慕雨', '暮色恋阳', '浅夏诗韵', '深秋墨香', '青禾', '暖阳',
        '清风徐来', '水波不兴', '云朵偷喝我酒', '月亮替我害羞', '半盏流年', '一抹浅笑', '素年锦时', '浅笑安然', '独宠一人', '唯爱一生',
        '霸者无敌', '王者独尊', '护妻狂魔', '宠夫达人', '一生只爱你一人', '此生唯你是我伴', '我的女人谁敢动', '我的男人我来宠', '天下为你', '江山如画',
        '独霸你的心', '独占你的爱', '王者归来', '佳人相伴', 'ヾ亲爱的→不离', 'ヾ宝贝儿→不弃', '笨蛋😉只牵你', '傻瓜😎只抱你', '余生❤唯爱你゛', '来世💗只念你゛',
        '甜系づ男孩', '萌系づ女孩', '星星⭐守护者', '月亮🌙陪伴者', '宠你ぐ一世ァ', '爱你ぐ一生ァ', '可爱😘小男友', '乖巧😚小女友', '我的♂私有物', '我的♀专属品',
        '阳光👦与你', '清风👧伴你', '暖男💗为你', '萌妹💖因你', '专属→你的爱💝', '独有→你的情💟', '酷仔😎的宝', '靓女😏的贝', '爱你👄没道理', '恋你💋不解释',
        '甜甜蜜蜜♂', '恩恩爱爱♀', '深情💑男主角', '深情💑女主角', '你的💌小情书', '我的💌小心事', '先生゛手给我', '小姐゛跟我走', '暖心❤大宝贝', '甜心💘小宝贝',
        '小熊🧸的怀抱', '小兔🐇的港湾', '帅气😏小哥哥', '漂亮😘小姐姐', '恋你💗的笨蛋', '爱你💕的傻瓜', '宝贝→抱抱😘', '宝宝→亲亲😚', '一生①世♂恋你', '一心一意♀爱你',
        '我的♂小甜心', '我的♀小暖男', '糖果🍬给你吃', '蛋糕🍰分你半', '午后☀的陪伴', '傍晚🌆的依偎', '亲亲😘小呆瓜', '抱抱😙小笨猪', '专属→小少爷', '专属→小小姐',
        '爱你的❤小丑', '恋你的💛公主', '你是♂我的星', '你是♀我的月', '温柔💗小先生', '可爱💖小女士', '男友力💪爆棚', '女友力💗满满', '宝贝づ手牵手', '宝宝づ心连心',
        '甜橙🍊先生', '草莓🍓小姐', '陪你💙看日出', '伴你💜看日落', '酷帅😎小狼狗', '软萌😚小奶猫', '你是♂我的命', '你是♀我的心', '我的♂小太阳', '我的♀小月亮',
        '爱你♂每一天', '想你♀每一分', '萌面😜小超人', '甜心😘小仙女', '亲亲😘小可爱', '抱抱😙小宝贝', '专属♂你的爱', '独有♀你的情', '温柔♂风与你', '浪漫♀云伴你',
        '帅气♂小王子', '美丽♀小公主', '我的♂小确幸', '我的♀小美好', '爱你💘不放手', '恋你💗不回头', '甜蜜♂小两口', '恩爱♀小夫妻', '宝贝♂笑一个', '宝宝♀抱一下',
        '你是♂我最爱', '你是♀我唯一', '阳光☀下的爱', '月光🌙下的情', '暖心♂小暖炉', '甜心♀小棉袄', '酷盖😎与萌妹', '潮男😏与甜妞', '爱你♂到永远', '恋你♀到永恒',
        '你的♂小跟班', '你的♀小尾巴', '深情♂只为你', '厚意♀独予你', '宝贝♂快过来', '宝宝♀别乱跑', '你是♂我的甜', '你是♀我的蜜', '帅气♂守护者', '美丽♀被守护者',
        '我的♂小心肝', '我的♀小宝贝', '爱你♂没够呢', '恋你♀没厌呀', '萌宠😻小男友', '甜宝😸小女友', '宝贝♂看这里', '宝宝♀来这里', '一生♂追随你', '一世♀陪伴你',
        '你的♂避风港', '你的♀栖息地', '甜蜜♂小情话', '恩爱♀小承诺', '酷仔♂的宝子', '靓女♀的亲爱的', '爱你♂入了骨', '恋你♀入了髓', '宝贝♂牵好啦', '宝宝♀抓好咯',
        '你是♂我的光', '你是♀我的暖', '帅气♂小男神', '美丽♀小女神', '我的♂小宝藏', '我的♀小财富', '爱你♂永不变', '恋你♀永不悔', '萌面😜小情圣', '甜心😘小情痴',
        '宝贝♂小懒虫', '宝宝♀小馋猫', '你是♂我的梦', '你是♀我的想', '温柔♂护花者', '可爱♀花朵儿', '我的♂小世界', '我的♀小天地', '爱你♂在心底', '恋你♀在心田',
        '甜蜜♂小恋曲', '恩爱♀小情歌', '酷帅😎小情人', '软萌😚小爱人', '宝贝♂来抱抱', '宝宝♀来亲亲', '一生♂只为你', '一世♀仅念你', '你的♂小依赖', '你的♀小依靠',
        '深情♂小公子', '厚意♀小千金', '宝贝♂小迷糊', '宝宝♀小糊涂', '你是♂我的念', '你是♀我的思', '帅气♂引领者', '美丽♀追随者', '我的♂小幸福', '我的♀小快乐',
        '爱你♂无尽头', '恋你♀无边界', '萌宠😻小宝贝', '甜宝😸小心肝', '宝贝♂小调皮', '宝宝♀小捣蛋', '你是♂我的宝', '你是♀我的贝', '帅气♂护花使', '美丽♀花仙子',
        '我的♂小憧憬', '我的♀小期待', '爱你♂超疯狂', '恋你♀超热烈', '宝贝♂小甜蜜', '宝宝♀小恩爱', '你是♂我的恋', '你是♀我的爱', '温柔♂小暖男', '可爱♀小萌女',
        '我的♂小幸运', '我的♀小福气', '爱你♂心满满', '恋你♀情悠悠', '萌面😜小帅哥', '甜心😘小美女', '宝贝♂小乖乖', '宝宝♀小巧巧', '你是♂我的伴', '你是♀我的侣',
        '帅气♂小英雄', '美丽♀小佳人', '我的♂小相思', '我的♀小相恋', '爱你♂不迟疑', '恋你♀不犹豫', '米花', '玉米花', '玉米绅士', '比心',
        '爱你', '喜欢你', '我爱你', '我喜欢你', '我只爱你', '我只喜欢你', '我永远爱你', '我永远喜欢你', '我最爱你', '我最喜欢你',
        '我好爱你', '我好喜欢你', '我超级爱你', '我超级喜欢你', '我非常爱你', '我非常喜欢你', '我真的爱你', '我真的喜欢你', '我太爱你了', '我太喜欢你了',
        '我好爱好爱你', '我好喜欢好喜欢你', '我超级超级爱你', '我超级超级喜欢你', '我永远永远爱你', '我永远永远喜欢你', '我最爱最爱你', '我最喜欢最喜欢你', '我的宝贝', '我的亲爱的',
        '我的小可爱', '我的小甜心', '我的小心肝', '我的小宝贝儿', '我的亲爱的宝贝', '我的小可爱宝贝', '我的小甜心宝贝', '我的小心肝宝贝', '我的宝贝儿', '我的亲爱的',
        '我的小可爱', '我的小甜心', '我的小心肝', '我的小宝贝儿', '我的亲爱的宝贝', '我的小可爱宝贝', '我的小甜心宝贝', '我的小心肝宝贝'
      ];
      
      // 爱心数组
      const hearts = [];
      let totalHearts = 400;
      
      // 烟花数组
      const fireworks = [];
      
      // 创建爱心
      function createHearts() {
        for (let i = 0; i < totalHearts; i++) {
          hearts.push({
            x: Math.random() * window.innerWidth,
            y: Math.random() * window.innerHeight,
            size: Math.random() * 25 + 5, // 大小不一的心型爱心
            color: `hsla(${Math.random() * 60 + 330}, ${Math.random() * 30 + 70}%, ${Math.random() * 20 + 60}%, ${Math.random() * 0.7 + 0.3})`, // 颜色随机
            speedX: (Math.random() - 0.5) * 2,
            speedY: (Math.random() - 0.5) * 2,
            rotation: Math.random() * Math.PI * 2,
            rotationSpeed: (Math.random() - 0.5) * 0.1,
            opacity: Math.random() * 0.7 + 0.3,
            opacitySpeed: (Math.random() - 0.5) * 0.01
          });
        }
      }
      
      // 绘制爱心
      function drawHeart(ctx, x, y, size, color, rotation, opacity) {
        ctx.save();
        ctx.translate(x, y);
        ctx.rotate(rotation);
        ctx.scale(size, size);
        ctx.globalAlpha = opacity;
        
        ctx.beginPath();
        ctx.moveTo(0, 0);
        ctx.bezierCurveTo(0.25, -0.1, 0.45, -0.25, 0.45, -0.5);
        ctx.bezierCurveTo(0.45, -0.75, 0.25, -1, 0, -1.25);
        ctx.bezierCurveTo(-0.25, -1, -0.45, -0.75, -0.45, -0.5);
        ctx.bezierCurveTo(-0.45, -0.25, -0.25, -0.1, 0, 0);
        ctx.closePath();
        
        ctx.fillStyle = color;
        ctx.fill();
        
        ctx.restore();
      }
      
      // 更新爱心
      function updateHearts() {
        heartsCtx.clearRect(0, 0, heartsCanvas.width, heartsCanvas.height);
        
        for (let heart of hearts) {
          heart.x += heart.speedX;
          heart.y += heart.speedY;
          heart.rotation += heart.rotationSpeed;
          heart.opacity += heart.opacitySpeed;
          
          // 边界检查
          if (heart.x < -50) heart.x = window.innerWidth + 50;
          if (heart.x > window.innerWidth + 50) heart.x = -50;
          if (heart.y < -50) heart.y = window.innerHeight + 50;
          if (heart.y > window.innerHeight + 50) heart.y = -50;
          
          // 透明度循环
          if (heart.opacity > 1) {
            heart.opacity = 1;
            heart.opacitySpeed *= -1;
          } else if (heart.opacity < 0.1) {
            heart.opacity = 0.1;
            heart.opacitySpeed *= -1;
          }
          
          // 绘制爱心
          drawHeart(heartsCtx, heart.x, heart.y, heart.size, heart.color, heart.rotation, heart.opacity);
        }
        
        requestAnimationFrame(updateHearts);
      }
      
      // 创建烟花
      function createFirework() {
        const x = Math.random() * window.innerWidth;
        const y = Math.random() * window.innerHeight;
        const size = Math.random() * 2 + 1;
        const isBig = Math.random() > 0.7; // 30%概率是大型烟花
        
        fireworks.push({
          x: x,
          y: y,
          size: isBig ? size * 2 : size,
          particles: [],
          exploded: false,
          explodeTimer: isBig ? 1000 : 500, // 大型烟花延迟更长
          created: Date.now(),
          isBig: isBig
        });
        
        // 如果是大型烟花，添加一些小的先导粒子
        if (isBig) {
          for (let i = 0; i < 10; i++) {
            fireworks[fireworks.length - 1].particles.push({
              x: x,
              y: y,
              size: Math.random() * 2 + 1,
              color: `hsl(${Math.random() * 30 + 330}, 100%, 70%)`,
              speedX: (Math.random() - 0.5) * 3,
              speedY: (Math.random() - 0.5) * 3,
              alpha: 1,
              alphaSpeed: 0.02
            });
          }
        }
      }
      
      // 更新烟花
      function updateFireworks() {
        fireworksCtx.clearRect(0, 0, fireworksCanvas.width, fireworksCanvas.height);
        
        // 移除已经完成的烟花
        fireworks.forEach((firework, index) => {
          if (firework.exploded && firework.particles.length === 0) {
            fireworks.splice(index, 1);
            return;
          }
          
          // 如果还没爆炸，绘制烟花引线
          if (!firework.exploded) {
            // 绘制引线
            fireworksCtx.beginPath();
            fireworksCtx.moveTo(firework.x, firework.y);
            fireworksCtx.lineTo(firework.x, firework.y + 20);
            fireworksCtx.strokeStyle = 'rgba(255, 255, 255, 0.6)';
            fireworksCtx.lineWidth = 2;
            fireworksCtx.stroke();
            
            // 绘制火花
            fireworksCtx.beginPath();
            fireworksCtx.arc(firework.x, firework.y, 3, 0, Math.PI * 2);
            fireworksCtx.fillStyle = 'rgba(255, 255, 255, 0.8)';
            fireworksCtx.fill();
            
            // 更新先导粒子
            if (firework.isBig) {
              firework.particles.forEach((particle, pIndex) => {
                particle.x += particle.speedX;
                particle.y += particle.speedY;
                particle.alpha -= particle.alphaSpeed;
                
                if (particle.alpha <= 0) {
                  firework.particles.splice(pIndex, 1);
                  return;
                }
                
                fireworksCtx.beginPath();
                fireworksCtx.arc(particle.x, particle.y, particle.size, 0, Math.PI * 2);
                fireworksCtx.fillStyle = `${particle.color.replace(')', `, ${particle.alpha})`)}`;
                fireworksCtx.fill();
              });
            }
            
            // 检查是否该爆炸
            if (Date.now() - firework.created > firework.explodeTimer) {
              explodeFirework(firework);
              firework.exploded = true;
            }
          } else {
            // 更新爆炸粒子
            firework.particles.forEach((particle, pIndex) => {
              particle.x += particle.speedX;
              particle.y += particle.speedY;
              particle.alpha -= particle.alphaSpeed;
              
              // 重力效果
              particle.speedY += 0.1;
              
              if (particle.alpha <= 0) {
                firework.particles.splice(pIndex, 1);
                return;
              }
              
              // 绘制粒子
              fireworksCtx.beginPath();
              fireworksCtx.arc(particle.x, particle.y, particle.size, 0, Math.PI * 2);
              fireworksCtx.fillStyle = `${particle.color.replace(')', `, ${particle.alpha})`)}`;
              fireworksCtx.fill();
              
              // 添加发光效果
              fireworksCtx.beginPath();
              fireworksCtx.arc(particle.x, particle.y, particle.size * 2, 0, Math.PI * 2);
              fireworksCtx.fillStyle = `${particle.color.replace(')', `, ${particle.alpha * 0.3})`)}`;
              fireworksCtx.fill();
            });
          }
        });
        
        requestAnimationFrame(updateFireworks);
      }
      
      // 爆炸烟花
      function explodeFirework(firework) {
        const particleCount = firework.isBig ? 200 : 100;
        const colors = firework.isBig ? [
          `hsl(${Math.random() * 30 + 330}, 100%, 70%)`,
          `hsl(${Math.random() * 30 + 0}, 100%, 70%)`,
          `hsl(${Math.random() * 30 + 30}, 100%, 70%)`
        ] : [`hsl(${Math.random() * 60 + 300}, 100%, 70%)`];
        
        for (let i = 0; i < particleCount; i++) {
          const angle = Math.random() * Math.PI * 2;
          const speed = Math.random() * (firework.isBig ? 5 : 3) + 1;
          const size = Math.random() * (firework.isBig ? 3 : 2) + 1;
          const color = colors[Math.floor(Math.random() * colors.length)];
          
          firework.particles.push({
            x: firework.x,
            y: firework.y,
            size: size,
            color: color,
            speedX: Math.cos(angle) * speed,
            speedY: Math.sin(angle) * speed,
            alpha: 1,
            alphaSpeed: 0.015
          });
        }
        
        // 添加中心闪光
        for (let i = 0; i < 20; i++) {
          firework.particles.push({
            x: firework.x,
            y: firework.y,
            size: Math.random() * 5 + 2,
            color: 'rgba(255, 255, 255, 0.9)',
            speedX: (Math.random() - 0.5) * 2,
            speedY: (Math.random() - 0.5) * 2,
            alpha: 1,
            alphaSpeed: 0.03
          });
        }
      }
      
      // 显示浪漫文字
      function showRomanticText() {
        const phoneContent = document.querySelector('.phone-content');
        const width = phoneContent.offsetWidth;
        const height = phoneContent.offsetHeight;
        
        const text = romanticTexts[Math.floor(Math.random() * romanticTexts.length)];
        const x = Math.random() * (width - 80) + 40;
        const y = Math.random() * (height - 40) + 20;
        const size = Math.random() * 15 + 15;
        const duration = Math.random() * 3000 + 2000;
        
        const textElement = document.createElement('div');
        textElement.className = 'romantic-text';
        textElement.textContent = text;
        textElement.style.left = `${x}px`;
        textElement.style.top = `${y}px`;
        textElement.style.fontSize = `${size}px`;
        
        romanticTextContainer.appendChild(textElement);
        
        // 动画
        gsap.to(textElement, {
          opacity: 1,
          duration: 0.5,
          onComplete: () => {
            setTimeout(() => {
              gsap.to(textElement, {
                opacity: 0,
                duration: 0.5,
                onComplete: () => {
                  romanticTextContainer.removeChild(textElement);
                }
              });
            }, duration);
          }
        });
      }
      
      // 显示比心动画
      function showHandHeart() {
        const phoneContent = document.querySelector('.phone-content');
        const width = phoneContent.offsetWidth;
        const height = phoneContent.offsetHeight;
        
        const x = Math.random() * (width - 80) + 40;
        const y = Math.random() * (height - 80) + 40;
        const size = Math.random() * 20 + 20;
        const rotation = Math.random() * 40 - 20; // -20到20度的随机旋转
        
        const handHeartElement = document.createElement('div');
        handHeartElement.className = 'hand-heart';
        handHeartElement.innerHTML = '🤍';
        handHeartElement.style.left = `${x}px`;
        handHeartElement.style.top = `${y}px`;
        handHeartElement.style.fontSize = `${size}px`;
        handHeartElement.style.transform = `rotate(${rotation}deg)`;
        
        handHeartsContainer.appendChild(handHeartElement);
        
        // 动画
        gsap.to(handHeartElement, {
          opacity: 1,
          scale: 1.2,
          duration: 0.3,
          onComplete: () => {
            gsap.to(handHeartElement, {
              opacity: 0,
              scale: 0.8,
              y: y - 50,
              duration: 0.7,
              onComplete: () => {
                handHeartsContainer.removeChild(handHeartElement);
              }
            });
          }
        });
      }
      
      // 创建粒子效果
      function createParticles() {
        const phoneContent = document.querySelector('.phone-content');
        const width = phoneContent.offsetWidth;
        const height = phoneContent.offsetHeight;
        
        const particleCount = 80;
        
        for (let i = 0; i < particleCount; i++) {
          const particle = document.createElement('div');
          particle.className = 'particle';
          
          // 随机位置
          const x = Math.random() * width;
          const y = Math.random() * height;
          
          // 随机大小
          const size = Math.random() * 4 + 1;
          
          // 随机动画延迟
          const delay = Math.random() * 10;
          
          // 随机透明度
          const opacity = Math.random() * 0.7 + 0.3;
          
          // 随机颜色
          const colors = [
            'rgba(255, 107, 139, 0.8)',
            'rgba(255, 179, 186, 0.8)',
            'rgba(255, 224, 230, 0.8)',
            'rgba(255, 255, 255, 0.8)'
          ];
          const color = colors[Math.floor(Math.random() * colors.length)];
          
          // 设置样式
          particle.style.left = `${x}px`;
          particle.style.top = `${y}px`;
          particle.style.width = `${size}px`;
          particle.style.height = `${size}px`;
          particle.style.backgroundColor = color;
          particle.style.boxShadow = `0 0 ${size * 2}px ${color}`;
          particle.style.animationDelay = `${delay}s`;
          particle.style.opacity = opacity;
          
          particlesContainer.appendChild(particle);
        }
      }
      
      // 显示最终表白文案
      function showFinalText() {
        // 添加缩放动画
        gsap.fromTo(finalTextContainer, 
          { 
            opacity: 0, 
            scale: 0.5,
            y: 50
          }, 
          { 
            opacity: 1, 
            scale: 1,
            y: 0,
            duration: 1,
            ease: "elastic.out(1, 0.3)"
          }
        );
        
        // 添加背景图片和样式
        finalTextContainer.style.backgroundImage = `url('https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/09deb20b126c4e2c9f299b122867d28e~tplv-a9rns2rl98-image.image?rcl=202511111222158343F5A91910809ECDA4&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1765426979&x-signature=%2FP%2B2Ymtnhz%2BnVPLZy2bdriz6%2F9c%3D')`;
        finalTextContainer.style.backgroundSize = 'cover';
        finalTextContainer.style.backgroundPosition = 'center';
        finalTextContainer.style.padding = '2rem';
        finalTextContainer.style.borderRadius = '1rem';
        finalTextContainer.style.boxShadow = '0 0 30px rgba(255, 107, 139, 0.5)';
        finalTextContainer.style.backdropFilter = 'blur(5px)';
        finalTextContainer.style.border = '2px solid rgba(255, 255, 255, 0.3)';
        
        // 添加心跳动画
        gsap.to(finalTextContainer, {
          scale: 1.05,
          duration: 1.5,
          repeat: -1,
          yoyo: true,
          ease: "power1.inOut"
        });
      }
      
      // 音频控制事件
      audioControl.addEventListener('click', function() {
        if (backgroundMusic.paused) {
          backgroundMusic.play();
          audioIcon.className = 'fa fa-pause audio-icon';
        } else {
          backgroundMusic.pause();
          audioIcon.className = 'fa fa-music audio-icon';
        }
      });
      
      // 初始化音频（仅设置参数，不自动播放）
      function initAudio() {
        // 设置音频参数，但不自动播放
        backgroundMusic.currentTime = 65; // 设置从65秒开始播放（副歌部分）
        backgroundMusic.volume = 0.3; // 设置音量为30%
      }
      
      // 点击爱心按钮事件
      function handleHeartClick() {
        // 隐藏封面
        gsap.to(cover, {
          opacity: 0,
          duration: 1,
          onComplete: () => {
            cover.style.pointerEvents = 'none';
          }
        });
        
        // 播放背景音乐（从副歌部分开始）
        backgroundMusic.currentTime = 65; // 确保从65秒开始播放
        backgroundMusic.volume = 0.3; // 确保音量为30%
        backgroundMusic.play();
        audioIcon.className = 'fa fa-pause audio-icon';
        
        // 创建粒子
        createParticles();
        
        // 创建爱心
        createHearts();
        
        // 开始爱心动画
        updateHearts();
        
        // 开始烟花动画
        updateFireworks();
        
        // 定时创建烟花（每2秒一次）
        setInterval(createFirework, 2000);
        
        // 定时显示浪漫文字（加快显示速度，让520个昵称都能显示）
        const textInterval = setInterval(showRomanticText, 100);
        
        // 定时显示比心动画
        const handHeartInterval = setInterval(showHandHeart, 1000);
        
        // 6秒后显示最终文案
        setTimeout(() => {
          clearInterval(textInterval);
          clearInterval(handHeartInterval);
          showFinalText();
          
          // 显示分享按钮
          setTimeout(() => {
            document.getElementById('share-btn').style.opacity = '1';
          }, 1000);
        }, 6000);
      }
      
      // 为爱心按钮添加触摸和点击事件
      heartBtn.addEventListener('click', handleHeartClick);
      heartBtn.addEventListener('touchstart', function(e) {
        e.preventDefault();
        handleHeartClick();
      }, { passive: false });
      
      // 优化Canvas性能
      function optimizeCanvas() {
        // 降低Canvas分辨率以提高性能
        const dpr = window.devicePixelRatio || 1;
        const phoneContent = document.querySelector('.phone-content');
        const width = phoneContent.offsetWidth;
        const height = phoneContent.offsetHeight;
        
        // 设置Canvas分辨率
        heartsCanvas.width = width * dpr;
        heartsCanvas.height = height * dpr;
        fireworksCanvas.width = width * dpr;
        fireworksCanvas.height = height * dpr;
        
        // 缩放Canvas以匹配设备分辨率
        heartsCanvas.style.width = width + 'px';
        heartsCanvas.style.height = height + 'px';
        fireworksCanvas.style.width = width + 'px';
        fireworksCanvas.style.height = height + 'px';
        
        // 缩放上下文以匹配设备分辨率
        heartsCtx.scale(dpr, dpr);
        fireworksCtx.scale(dpr, dpr);
        
        // 减少爱心数量以提高性能
        totalHearts = Math.floor(totalHearts * 0.7);
      }
      
      // 分享功能
      function initShare() {
        const shareBtn = document.getElementById('share-btn');
        const shareToast = document.getElementById('share-toast');
        
        // 隐藏分享按钮
        shareBtn.style.opacity = '0';
        
        // 分享按钮点击事件
        shareBtn.addEventListener('click', function() {
          // 显示分享提示
          shareToast.style.opacity = '1';
          
          // 3秒后隐藏提示
          setTimeout(() => {
            shareToast.style.opacity = '0';
          }, 3000);
          
          // 尝试使用Web Share API
          if (navigator.share) {
            navigator.share({
              title: '浪漫表白 - 汤晓慧专属',
              text: '这是我给你的专属浪漫表白',
              url: window.location.href
            }).catch(err => {
              console.log('分享失败:', err);
            });
          }
        });
        
        // 为分享按钮添加触摸事件
        shareBtn.addEventListener('touchstart', function(e) {
          e.preventDefault();
          shareBtn.click();
        }, { passive: false });
      }
      
      // 初始化
      function init() {
        // 优化Canvas性能
        optimizeCanvas();
        
        // 调整Canvas尺寸
        resizeCanvas();
        window.addEventListener('resize', resizeCanvas);
        
        // 初始化分享功能
        initShare();
        
        // 初始化音频
        initAudio();
        
        // 隐藏加载动画
        setTimeout(() => {
          const loader = document.getElementById('loader');
          gsap.to(loader, {
            opacity: 0,
            duration: 0.5,
            onComplete: () => {
              loader.style.display = 'none';
            }
          });
        }, 1000);
      }
      
      // 页面加载完成后初始化
      window.addEventListener('load', init);
    });
  </script>
</body>
</html>
