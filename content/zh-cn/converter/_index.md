---
title: "激素换算器"
description: "激素换算器"
date: 2020-10-26T04:15:05+08:00
draft: false
---

<div style="
  position: relative;
  display: flex;
  flex-direction: column;
  ">
  <style>
    input {
      color: #495057;
      border: 1px solid #ced4da;
      border-radius: 0.25rem;
      /*transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;*/
      padding: 1px;
      height: 1.5em;
    }

    select {
      color: #495057;
      border: 1px solid #ced4da;
      border-radius: 0.25rem;
      /*transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;*/
      padding: 1px;
      height: 1.5em;
    }

    input:focus {
      color: #495057;
      outline: 0;
      border-image: url(/images/shadow-i.png) 30 30 stretch;
      border-image-width: 3px;
      border-image-outset: 0px;
    }

  </style>
  <div style="margin:auto;align-items:baseline">
    <span>原数据：</span>
    <input type="text" id="val1" onkeyup="changed()" style="width: 10ex" />
    <select id="in1" oninput="changed()">
      <option value="1">pg</option>
      <option value="1000">ng</option>
      <option value="1000000">μg</option>
      <option value="mol">pmol</option>
      <option value="mol1000">nmol</option>
      <option value="mIU">mIU</option>
      <option value="uIU">μIU</option>
    </select>
    <span>/</span>
    <select id="in2" oninput="changed()">
      <option value="1">mL</option>
      <option value="100">dL</option>
      <option value="1000">L</option>
    </select>
    <select id="in3" oninput="changed()" style="visibility: hidden;">
      <option value="272.38">雌二醇</option>
      <option value="288.43">睾酮</option>
      <option value="23000">泌乳素</option>
      <option value="314.46">孕酮</option>
    </select>
    <select id="in4" oninput="changed()" style="visibility: hidden;">
      <option value="47170">泌乳素</option>
      <option value="113880">卵泡刺激素</option>
      <option value="46.56">促黄体素</option>
    </select>
  </div>
  <div style="margin:auto;">
    <span>转换为：</span>
    <input id="result" style="width: 10ex" value="" readonly="true" />
    <select id="out1" oninput="changed()">
      <option value="1">pg</option>
      <option value="1000">ng</option>
      <option value="1000000">μg</option>
      <option value="mol">pmol</option>
      <option value="mol1000">nmol</option>
    </select>
    <span>/</span>
    <select id="out2" oninput="changed()">
      <option value="1">mL</option>
      <option value="100">dL</option>
      <option value="1000">L</option>
    </select>
  </div>
</div>
<script type="text/javascript">
  function changed() {
    var val = Number(window.document.getElementById("val1").value);
    var in1 = window.document.getElementById("in1").value;
    var in2 = window.document.getElementById("in2").value;
    var in3 = Number(window.document.getElementById("in3").value);
    var in4 = Number(window.document.getElementById("in4").value);
    var out1 = window.document.getElementById("out1").value;
    var out2 = window.document.getElementById("out2").value;
    window.document.getElementById("in3").style.visibility = "hidden";
    window.document.getElementById("in4").style.visibility = "hidden";
    switch (in1) {
      case "mol":
        window.document.getElementById("in3").style.visibility = "visible";
        val = val * in3;
        break;
      case "mol1000":
        window.document.getElementById("in3").style.visibility = "visible";
        val = val * 1000 * in3;
        break;
      case "mIU":
        window.document.getElementById("in4").style.visibility = "visible";
        val = val * in4;
        break;
      case "uIU":
        window.document.getElementById("in4").style.visibility = "visible";
        val = val * in4 / 1000;
        break;
      default:
        //window.document.getElementById("in3").style.visibility = "hidden";
        val = val * Number(in1);
    }
    switch (out1) {
      case "mol":
        window.document.getElementById("in3").style.visibility = "visible";
        val = val / in3;
        break;
      case "mol1000":
        window.document.getElementById("in3").style.visibility = "visible";
        val = (val * 0.001) / in3;
        break;
      default:
        //window.document.getElementById("in3").style.visibility = "hidden";
        val = val / Number(out1);
    }
    val = (val * out2) / in2;
    if (isNaN(val)) {
      window.document.getElementById("result").value = "数值错误"; //输出
    } else {
      window.document.getElementById("result").value = val; //输出
    }
    return;
  }
</script>

&nbsp;

&nbsp;

---

注：部分医院可能使用[IU（国际单位）](https://zh.wikipedia.org/zh-hans/%E5%9B%BD%E9%99%85%E5%8D%95%E4%BD%8D)作为衡量激素水平的单位，但由于IU为医学效价单位，其与质量单位的换算取决于药物种类且可能随时间变化，在此仅提供部分参考。详见 [单位科普 - 国际单位（IU）]({{< ref "science-literacy#国际单位iu" >}})