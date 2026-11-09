<!DOCTYPE html>
<html lang="zhCN">
<head>
    <meta charset="UTF8">
    <meta name="viewport" content="width=devicewidth, initialscale=1.0">
    <title>《通用技术概论》智能学伴</title>
    <style>
        *{boxsizing:borderbox;margin:0;padding:0;fontfamily:"Microsoft Yahei",sansserif;}
        body{background:#f4f7fa;padding:20px;maxwidth:900px;margin:0 auto;}
        .container{background:#fff;borderradius:12px;boxshadow:0 2px 12px #00000015;overflow:hidden;}
        .header{background:#2b5797;color:#fff;padding:16px;textalign:center;fontsize:20px;fontweight:bold;}
        .chatwindow{height:450px;padding:16px;overflowy:auto;background:#fafbfc;}
        .msguser{margin:10px 0;textalign:right;}
        .msguser .content{display:inlineblock;background:#2b5797;color:white;padding:10px 14px;borderradius:12px;maxwidth:75%;}
        .msgbot{margin:10px 0;textalign:left;}
        .msgbot .content{display:inlineblock;background:#e8edf4;color:#222;padding:10px 14px;borderradius:12px;maxwidth:75%;}
        .inputarea{display:flex;padding:14px;bordertop:1px solid #eee;gap:8px;}
        #userInput{flex:1;padding:10px 12px;border:1px solid #ccc;borderradius:8px;fontsize:15px;}
        #sendBtn{padding:10px 20px;background:#2b5797;color:white;border:none;borderradius:8px;cursor:pointer;}
        .tip{padding:12px 16px;color:#666;fontsize:14px;background:#f0f4f9;}
    </style>
</head>
<body>
<div class="container">
    <div class="header">《通用技术概论》课程智能学伴</div>
    <div class="tip">💡可提问：知识点答疑、预习提纲、习题练习、技术设计案例、作业思路提示</div>
    <div class="chatwindow" id="chatBox">
        <div class="msgbot">
            <div class="content">你好！我是《通用技术概论》智能学伴。你可以向我咨询课程知识点、预习复习、技术设计案例、作业思路等问题。</div>
        </div>
    </div>
    <div class="inputarea">
        <input type="text" id="userInput" placeholder="请输入你的问题...">
        <button id="sendBtn">发送</button>
    </div>
</div>

<script>
const chatBox = document.getElementById("chatBox");
const userInput = document.getElementById("userInput");
const sendBtn = document.getElementById("sendBtn");

// 简易本地智能体知识库
const knowledge = {
    "预习":"课前预习建议：重点阅读教材技术的性质、技术设计原则章节；思考技术与人、社会、自然之间的关系，可列出3个生活中的技术产品。",
    "复习":"课后复习要点：掌握技术的5个性质、设计的一般原则、工艺基础；区分技术发明与技术革新，梳理实践设计项目流程。",
    "技术性质":"技术具有目的性、创新性、综合性、两面性、专利性。目的性指技术为解决特定问题产生；创新性包含发明和革新；综合性融合多学科知识；两面性有有利也存在隐患；专利性保护技术创新成果。",
    "设计原则":"设计一般原则包含创新、实用、经济、美观、道德、技术规范、可持续发展，各原则之间相互联系、相互制约。",
    "作业":"我不会直接提供完整作业答案，可以给你思路提示，请告诉我是哪一道作业题目。",
    "案例":"生活技术设计案例：便携折叠购物篮、可调节高度书桌、简易雨水收集装置，在设计时需要兼顾实用、成本、美观与可持续发展。",
    "实践":"技术设计实践流程：发现与明确问题 → 制定设计方案 → 制作模型或原型 → 测试评估及优化 → 产品使用维护说明。",
    "发明":"技术发明：创造自然界从来没有的事物；技术革新：在原有技术基础之上改进提升。"
};

function botReply(q){
    let qs = q.trim().toLowerCase();
    for(let key in knowledge){
        if(qs.includes(key)) return knowledge[key];
    }
    return "我是课程辅助学伴，你可以询问通用技术概论相关知识点、预习复习、设计案例、作业思路提示。请换一个课程相关问题提问。";
}

function addMsg(text,isUser){
    const div = document.createElement("div");
    div.className = isUser?"msguser":"msgbot";
    div.innerHTML = `<div class="content">${text}</div>`;
    chatBox.appendChild(div);
    chatBox.scrollTop = chatBox.scrollHeight;
}

function send(){
    let text = userInput.value.trim();
    if(!text) return;
    addMsg(text,true);
    userInput.value="";
    setTimeout(()=>{
        addMsg(botReply(text),false);
    },400);
}

sendBtn.onclick = send;
userInput.onkeydown = e=>{if(e.key==="Enter") send();};
</script>
</body>
</html>
