<template>
  <div class="hello">

    <!--Echarts图表盒子-->
    <div id="myChart" :style="{width: '1633px', height: '300px'}"></div>
    <!--表格-->
    <div style="margin-left: 3px;width: 1633px;">
      <table style="border: 1px solid blue;" id="infotableid">
        <!--住院天数-->
        <!--<tr>-->
        <!--<td style="text-align: right;" colspan="2">住院天数</td>-->
        <!--<td v-for="dayS in dayS" style="width: 142px;text-align: center;font-size: 12px;">{{dayS}}</td>-->
        <!--</tr>-->
        <tr>
          <td style="text-align: right;" colspan="2">疼痛评分</td>
          <td v-for="dayS in FixedGuardianshipChartInfoList" style="width: 142px;text-align: center;font-size: 12px;"><span v-for="PainLevelListdata in dayS.PainLevelList">{{PainLevelListdata}}&nbsp;</span></td>
        </tr>
        <tr>
          <td style="text-align: right;" colspan="2">住院天数</td>
          <td v-for="dayS in FixedGuardianshipChartInfoList" style="width: 142px;text-align: center;font-size: 12px;">{{dayS.InhsopCount}}</td>
        </tr>
        <tr>
          <td colspan="2"  style="text-align: right;">呼吸（次/分）</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length>0" v-for="Breathings in FixedGuardianshipChartInfoList" style="width: 135px;">{{Breathings.Breathing}}</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length==0" v-for="cellength in [1,2,3,4,5,6,7,8,9,10]"></td>
        </tr>


        <tr>
          <td rowspan="4">
            出量
          </td>
          <td style="text-align: right;">小便量（ml）</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length>0" v-for="OuputClss in FixedGuardianshipChartInfoList" style="">{{OuputClss.OuputCls.UrineVolume}}</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length==0" v-for="cellength in [1,2,3,4,5,6,7,8,9,10]"></td>
        </tr>
        <tr>
          <td style="text-align: right;">大便（次）</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length>0"  v-for="OuputClss in FixedGuardianshipChartInfoList" style="">{{OuputClss.OuputCls.StoolTimes}}</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length==0" v-for="cellength in [1,2,3,4,5,6,7,8,9,10]"></td>
        </tr>
        <tr>
          <td style="text-align: right;">引流量（ml）</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length>0"  v-for="OuputClss in FixedGuardianshipChartInfoList" style="">{{OuputClss.OuputCls.InducedFlow}}</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length==0" v-for="cellength in [1,2,3,4,5,6,7,8,9,10]"></td>
        </tr>
        <tr>
          <td style="text-align: right;">其他（ml）</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length>0"  v-for="OuputClss in FixedGuardianshipChartInfoList" style="">{{OuputClss.OuputCls.Other}}</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length==0" v-for="cellength in [1,2,3,4,5,6,7,8,9,10]"></td>
        </tr>

        <!--入量-->
        <tr>
          <td rowspan="2">
            入量
          </td>
          <td style="text-align: right;">饮入量（ml）</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length>0"  v-for="InputClsobject in FixedGuardianshipChartInfoList" style="">{{InputClsobject.InputCls.Intake}}</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length==0" v-for="cellength in [1,2,3,4,5,6,7,8,9,10]"></td>
        </tr>
        <tr>
          <td style="text-align: right;">输入量（ml）</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length>0"  v-for="InputClsobject in FixedGuardianshipChartInfoList" style="">{{InputClsobject.InputCls.Input}}</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length==0" v-for="cellength in [1,2,3,4,5,6,7,8,9,10]"></td>
        </tr>

        <!--血压-->
        <tr>
          <td rowspan="2">
            血压
          </td>
          <td style="text-align: right;">收缩压（mmHg）</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length>0"  v-for="BloodPressureDetailobj in FixedGuardianshipChartInfoList" style="">{{BloodPressureDetailobj.BloodPressureDetail.SystolicPressure}}</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length==0" v-for="cellength in [1,2,3,4,5,6,7,8,9,10]"></td>
        </tr>
        <tr>
          <td style="text-align: right;">舒张压（mmHg）</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length>0"  v-for="BloodPressureDetailobj in FixedGuardianshipChartInfoList" style="">{{BloodPressureDetailobj.BloodPressureDetail.DiastolicPressure}}</td>
          <td v-if="FixedGuardianshipChartInfoList.length!==undefined && FixedGuardianshipChartInfoList.length==0" v-for="cellength in [1,2,3,4,5,6,7,8,9,10]"></td>
        </tr>

        <!--手术-->
        <!--<tr>-->
          <!--<td  style="text-align: right;" colspan="2">手术</td>-->
          <!--<td  v-for="OperationInfoListinfo in OperationInfoList" style="">-->
                <!--<span class="iconcolor OperationBacImg" v-if="OperationInfoListinfo.IsUse">-->
                  <!--<p class="tdtip">-->
                    <!--<span  v-for="OprLists in OperationInfoListinfo.OprList" v-if="OprLists.IsUse">{{OprLists.OprInfo}}<br></span>-->
                  <!--</p>-->
                <!--</span>-->
          <!--</td>-->
          <!--<td v-if="OperationInfoList.length!==undefined && OperationInfoList.length==0" v-for="cellength in [1,2,3,4,5,6,7,8,9,10]"></td>-->
        <!--</tr>-->

        <!--病原学送检申请-->
        <!--<tr>-->
          <!--<td  style="text-align: right;" colspan="2">病原学送检申请</td>-->
          <!--<td  v-for="PathogenicExaminationListinfo in PathogenicExaminationList" style="">-->
                <!--<span class="PEiconcolor" v-if="PathogenicExaminationListinfo.IsUse" style="color: green">-->
                  <!--检-->
                  <!--<p class="PEtdtip">-->
                    <!--<span  v-for="PElist in PathogenicExaminationListinfo.ExamList" v-if="PElist.IsUse">-->
                      <!--{{PElist.RequestNo}}&nbsp;-->
                      <!--{{PElist.SamplingTime}}&nbsp;-->
                      <!--{{PElist.LabName}}&nbsp;-->
                      <!--{{PElist.ReportTime}}&nbsp;-->
                      <!--{{PElist.LabResult}}&nbsp;-->
                      <!--<br></span>-->
                  <!--</p>-->
                <!--</span>-->
          <!--</td>-->
          <!--<td v-if="PathogenicExaminationList.length!==undefined && PathogenicExaminationList.length==0" v-for="cellength in [1,2,3,4,5,6,7,8,9,10]"></td>-->
        <!--</tr>-->

        <!--药品-->
        <tr v-for="DrugNameArrays in YAntibacterialDrugList">
          <td  style="text-align: right;" colspan="2">{{DrugNameArrays.DrugName}}</td>
          <td  v-for="tableDatainfo in AntibacterialDrugList">
                          <span class="Drugiconcolor" v-for="drugs in tableDatainfo.AntibacterialDrugList" v-if="drugs.DrugCode==DrugNameArrays.DrugCode&&drugs.IsUse">
                            <span class="Drugtdtip">
                              <!--<span v-if="drugs.IsTemp==1">【临】&nbsp;&nbsp;</span>-->
                              <!--<span v-if="drugs.IsTemp==0">【长】&nbsp;&nbsp;</span>-->
                              {{drugs.DrugInfo}}
                            </span>
                          </span>
          </td>
        </tr>

        <!--自定义项目检验结果项目-->
        <tr v-for="defineLabNameArrays in YUserDefineLabList">
          <td  style="text-align: right;" colspan="2">{{defineLabNameArrays.ItemName}}</td>
          <td  v-for="UserDefineLabListinfo in UserDefineLabList">
                          <span class="Drugiconcolor" v-for="DefineLabS in UserDefineLabListinfo.UserDefineLabList" v-if="DefineLabS.ItemCode==defineLabNameArrays.ItemCode&&DefineLabS.IsUse">
                            <!--<span class="Drugtdtip">{{DefineLabS.LabInfo}}</span>-->
                            <span class="Drugtdtip">
                              <span>{{DefineLabS.TakeTime}}&nbsp;</span>
                              <!--<span>{{DefineLabS.LabResult}}&nbsp;</span>-->
                              <span v-if="DefineLabS.ResultFlag=='H'" style="color: red;">{{DefineLabS.LabResult}}&nbsp; ↑&nbsp; </span>
                              <span v-if="DefineLabS.ResultFlag=='M'">{{DefineLabS.LabResult}}</span>
                              <span v-if="DefineLabS.ResultFlag=='L'" style="color: red;">{{DefineLabS.LabResult}}&nbsp;↓&nbsp; </span>
                              <span v-if="DefineLabS.ResultFlag=='P'" style="color: red;">{{DefineLabS.LabResult}}&nbsp;阳性&nbsp; </span>
                              <span v-if="DefineLabS.ResultFlag=='Q'" style="color: red;">{{DefineLabS.LabResult}}&nbsp;弱阳性&nbsp; </span>
                              <span v-if="DefineLabS.ResultFlag=='N'" style="color: red;">{{DefineLabS.LabResult}}&nbsp;阴性&nbsp; </span>
                              <span v-if="DefineLabS.ResultFlag=='E'" style="color: red;">{{DefineLabS.LabResult}}&nbsp;错误&nbsp; </span>
                              <span>（{{DefineLabS.Range}}）&nbsp; </span>
                              <span>{{DefineLabS.Unit}}&nbsp; </span>
                            </span>
                          </span>
          </td>
        </tr>

        <!--自定义项目药品-->
        <tr v-for="YUserDefineDrugListNameArrays in YUserDefineDrugList">
          <td style="" colspan="2">{{YUserDefineDrugListNameArrays.DrugName}}</td>
          <td  v-for="UserDefineLabListinfo in UserDefineDrugList">
                          <span class="Drugiconcolor" v-for="UserDefineDrugListS in UserDefineLabListinfo.UserDefineDrugList" v-if="UserDefineDrugListS.DrugCode==YUserDefineDrugListNameArrays.DrugCode&&UserDefineDrugListS.IsUse">
                            <span class="Drugtdtip">{{UserDefineDrugListS.DrugInfo}}</span>
                          </span>
          </td>
        </tr>

      </table>
    </div>

  </div>
</template>

<script>
  export default {
    name: 'hello',
    data () {
      return {
        AntibacterialDrugList: [],
        YAntibacterialDrugList: [],//药品y轴
        /*每天固定所有数据*/
        FixedGuardianshipChartInfoList: [
            {
          Date: "2019-09-28",//日期
          InhsopCount: "40",//住院天数
          Pulse: "100",//脉搏
          Breathing: "20",//呼吸
          Temperature: "36",//体温
          /*出量*/
          OuputCls: {
            UrineVolume: "10",
            StoolTimes: "20",
            InducedFlow: "30",
            Other: "40"
          },
          /*入量*/
          InputCls: {
            Intake: "50",
            Input: "60"
          },
          /*血压*/
          BloodPressureDetail: {
            SystolicPressure: "70",
            DiastolicPressure: "80"
          },
          PainLevelList: [3]//疼痛评分
        }, {
          Date: "2019-09-29",
          InhsopCount: "41",
          Pulse: "90",
          Breathing: "63",
          Temperature: "40",
              /*出量*/
              OuputCls: {
                UrineVolume: "10",
                StoolTimes: "20",
                InducedFlow: "30",
                Other: "40"
              },
              /*入量*/
              InputCls: {
                Intake: "50",
                Input: "60"
              },
              /*血压*/
              BloodPressureDetail: {
                SystolicPressure: "70",
                DiastolicPressure: "80"
              },
              PainLevelList: [3]//疼痛评分
        }, {
          Date: "2019-09-30",
          InhsopCount: "42",
          Pulse: "80",
          Breathing: "62",
          Temperature: "38",
              /*出量*/
              OuputCls: {
                UrineVolume: "10",
                StoolTimes: "20",
                InducedFlow: "30",
                Other: "40"
              },
              /*入量*/
              InputCls: {
                Intake: "50",
                Input: "60"
              },
              /*血压*/
              BloodPressureDetail: {
                SystolicPressure: "70",
                DiastolicPressure: "80"
              },
              PainLevelList: [3]//疼痛评分
        }, {
          Date: "2019-10-01",
          InhsopCount: "43",
          Pulse: "80",
          Breathing: "15",
          Temperature: "35",
              /*出量*/
              OuputCls: {
                UrineVolume: "10",
                StoolTimes: "20",
                InducedFlow: "30",
                Other: "40"
              },
              /*入量*/
              InputCls: {
                Intake: "50",
                Input: "60"
              },
              /*血压*/
              BloodPressureDetail: {
                SystolicPressure: "70",
                DiastolicPressure: "80"
              },
              PainLevelList: [3]//疼痛评分
        }, {
          Date: "2019-10-02",
          InhsopCount: "44",
          Pulse: "120",
          Breathing: "14",
          Temperature: "37",
              /*出量*/
              OuputCls: {
                UrineVolume: "10",
                StoolTimes: "20",
                InducedFlow: "30",
                Other: "40"
              },
              /*入量*/
              InputCls: {
                Intake: "50",
                Input: "60"
              },
              /*血压*/
              BloodPressureDetail: {
                SystolicPressure: "70",
                DiastolicPressure: "80"
              },
              PainLevelList: [3]//疼痛评分
        }, {
          Date: "2019-10-03",
          InhsopCount: "45",
          Pulse: "80",
          Breathing: "36",
          Temperature: "37",
              /*出量*/
              OuputCls: {
                UrineVolume: "10",
                StoolTimes: "20",
                InducedFlow: "30",
                Other: "40"
              },
              /*入量*/
              InputCls: {
                Intake: "50",
                Input: "60"
              },
              /*血压*/
              BloodPressureDetail: {
                SystolicPressure: "70",
                DiastolicPressure: "80"
              },
              PainLevelList: [3]//疼痛评分
        }, {
          Date: "2019-10-04",
          InhsopCount: "46",
          Pulse: "90",
          Breathing: "33",
          Temperature: "35",
              /*出量*/
              OuputCls: {
                UrineVolume: "10",
                StoolTimes: "20",
                InducedFlow: "30",
                Other: "40"
              },
              /*入量*/
              InputCls: {
                Intake: "50",
                Input: "60"
              },
              /*血压*/
              BloodPressureDetail: {
                SystolicPressure: "70",
                DiastolicPressure: "80"
              },
              PainLevelList: [3]//疼痛评分
        }, {
          Date: "2019-10-05",
          InhsopCount: "47",
          Pulse: "80",
          Breathing: "34",
          Temperature: "38",
              /*出量*/
              OuputCls: {
                UrineVolume: "10",
                StoolTimes: "20",
                InducedFlow: "30",
                Other: "40"
              },
              /*入量*/
              InputCls: {
                Intake: "50",
                Input: "60"
              },
              /*血压*/
              BloodPressureDetail: {
                SystolicPressure: "70",
                DiastolicPressure: "80"
              },
              PainLevelList: [3]//疼痛评分
        }, {
          Date: "2019-10-06",
          InhsopCount: "48",
          Pulse: "70",
          Breathing: "52",
          Temperature: "35",
              /*出量*/
              OuputCls: {
                UrineVolume: "10",
                StoolTimes: "20",
                InducedFlow: "30",
                Other: "40"
              },
              /*入量*/
              InputCls: {
                Intake: "50",
                Input: "60"
              },
              /*血压*/
              BloodPressureDetail: {
                SystolicPressure: "70",
                DiastolicPressure: "80"
              },
              PainLevelList: [3]//疼痛评分
        }, {
          Date: "2019-10-07",
          InhsopCount: "49",
          Pulse: "110",
          Breathing: "11",
          Temperature: "37",
              /*出量*/
              OuputCls: {
                UrineVolume: "10",
                StoolTimes: "20",
                InducedFlow: "30",
                Other: "40"
              },
              /*入量*/
              InputCls: {
                Intake: "50",
                Input: "60"
              },
              /*血压*/
              BloodPressureDetail: {
                SystolicPressure: "70",
                DiastolicPressure: "80"
              },
              PainLevelList: [3]//疼痛评分
        }, {
          Date: "2019-10-08",
          InhsopCount: "50",
          Pulse: "90",
          Breathing: "12",
          Temperature: "36",
              /*出量*/
              OuputCls: {
                UrineVolume: "10",
                StoolTimes: "20",
                InducedFlow: "30",
                Other: "40"
              },
              /*入量*/
              InputCls: {
                Intake: "50",
                Input: "60"
              },
              /*血压*/
              BloodPressureDetail: {
                SystolicPressure: "70",
                DiastolicPressure: "80"
              },
              PainLevelList: [3]//疼痛评分
        }, {
          Date: "2019-10-09",
          InhsopCount: "51",
          Pulse: "70",
          Breathing: "14",
          Temperature: "38.8",
              /*出量*/
              OuputCls: {
                UrineVolume: "10",
                StoolTimes: "20",
                InducedFlow: "30",
                Other: "40"
              },
              /*入量*/
              InputCls: {
                Intake: "50",
                Input: "60"
              },
              /*血压*/
              BloodPressureDetail: {
                SystolicPressure: "70",
                DiastolicPressure: "80"
              },
              PainLevelList: [3]//疼痛评分
        }, {
          Date: "2019-10-10",
          InhsopCount: "52",
          Pulse: "70",
          Breathing: "15",
          Temperature: "36",
              /*出量*/
              OuputCls: {
                UrineVolume: "10",
                StoolTimes: "20",
                InducedFlow: "30",
                Other: "40"
              },
              /*入量*/
              InputCls: {
                Intake: "50",
                Input: "60"
              },
              /*血压*/
              BloodPressureDetail: {
                SystolicPressure: "70",
                DiastolicPressure: "80"
              },
              PainLevelList: [3]//疼痛评分
        }, {
          Date: "2019-10-11",
          InhsopCount: "53",
          Pulse: "90",
          Breathing: "30",
          Temperature: "36.5",
              /*出量*/
              OuputCls: {
                UrineVolume: "10",
                StoolTimes: "20",
                InducedFlow: "30",
                Other: "40"
              },
              /*入量*/
              InputCls: {
                Intake: "50",
                Input: "60"
              },
              /*血压*/
              BloodPressureDetail: {
                SystolicPressure: "70",
                DiastolicPressure: "80"
              },
              PainLevelList: [3]//疼痛评分
        }, {
          Date: "2019-10-12",
          InhsopCount: "54",
          Pulse: "80",
          Breathing: "25",
          Temperature: "36.5",
              /*出量*/
              OuputCls: {
                UrineVolume: "10",
                StoolTimes: "20",
                InducedFlow: "30",
                Other: "40"
              },
              /*入量*/
              InputCls: {
                Intake: "50",
                Input: "60"
              },
              /*血压*/
              BloodPressureDetail: {
                SystolicPressure: "70",
                DiastolicPressure: "80"
              },
              PainLevelList: [3]//疼痛评分
        }],
        /*手术*/
        OperationInfoList: [],
        /*病原学送检申请*/
        PathogenicExaminationList: [],
        /*自定义药品X轴药品使用数据情况循环，加hover标注了用药途径*/
        UserDefineDrugList: [
          {
            Date: "2019-09-28",
            UserDefineDrugList: [
            {
              DrugCode: "Y00000000668",
              DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
              IsTemp: 0,
              IsUse: false//是否显示划线背景
            }, {
              DrugCode: "Y00000000532",
              DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
              IsTemp: 0,
              IsUse: true
            },
              {
                DrugCode: "Y00000000667",
                DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
                IsTemp: 0,
                IsUse: false
              }, {
                DrugCode: "Y00000000537",
                DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
                IsTemp: 0,
                IsUse: true
              }
            ]
        }, {
          Date: "2019-09-29",
          UserDefineDrugList: [{
            DrugCode: "Y00000000668",
            DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
            IsTemp: 0,
            IsUse: false
          }, {
            DrugCode: "Y00000000537",
            DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
            IsTemp: 0,
            IsUse: true
          },
            {
              DrugCode: "Y00000000667",
              DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
              IsTemp: 0,
              IsUse: false
            }, {
              DrugCode: "Y00000000532",
              DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
              IsTemp: 0,
              IsUse: true
            }]
        }, {
          Date: "2019-09-30",
          UserDefineDrugList: [{
            DrugCode: "Y00000000668",
            DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
            IsTemp: 0,
            IsUse: false
          }, {
            DrugCode: "Y00000000532",
            DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
            IsTemp: 0,
            IsUse: true
          },
            {
              DrugCode: "Y00000000667",
              DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
              IsTemp: 0,
              IsUse: false
            }, {
              DrugCode: "Y00000000537",
              DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
              IsTemp: 0,
              IsUse: true
            }]
        }, {
          Date: "2019-10-01",
          UserDefineDrugList: [{
            DrugCode: "Y00000000668",
            DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
            IsTemp: 0,
            IsUse: false
          }, {
            DrugCode: "Y00000000532",
            DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
            IsTemp: 0,
            IsUse: false
          },
            {
              DrugCode: "Y00000000667",
              DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
              IsTemp: 0,
              IsUse: false
            }, {
              DrugCode: "Y00000000537",
              DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
              IsTemp: 0,
              IsUse: false
            }]
        }, {
          Date: "2019-10-02",
          UserDefineDrugList: [{
            DrugCode: "Y00000000668",
            DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
            IsTemp: 0,
            IsUse: true
          }, {
            DrugCode: "Y00000000532",
            DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
            IsTemp: 0,
            IsUse: false
          },
            {
              DrugCode: "Y00000000667",
              DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
              IsTemp: 0,
              IsUse: true
            }, {
              DrugCode: "Y00000000537",
              DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
              IsTemp: 0,
              IsUse: false
            }]
        }, {
          Date: "2019-10-03",
          UserDefineDrugList: [{
            DrugCode: "Y00000000668",
            DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
            IsTemp: 0,
            IsUse: true
          }, {
            DrugCode: "Y00000000532",
            DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
            IsTemp: 0,
            IsUse: false
          },
            {
              DrugCode: "Y00000000667",
              DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
              IsTemp: 0,
              IsUse: true
            }, {
              DrugCode: "Y00000000537",
              DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
              IsTemp: 0,
              IsUse: false
            }]
        }, {
          Date: "2019-10-04",
          UserDefineDrugList: [{
            DrugCode: "Y00000000668",
            DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
            IsTemp: 0,
            IsUse: true
          }, {
            DrugCode: "Y00000000532",
            DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
            IsTemp: 0,
            IsUse: false
          },
            {
              DrugCode: "Y00000000667",
              DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
              IsTemp: 0,
              IsUse: true
            }, {
              DrugCode: "Y00000000537",
              DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
              IsTemp: 0,
              IsUse: false
            }]
        }, {
          Date: "2019-10-05",
          UserDefineDrugList: [{
            DrugCode: "Y00000000668",
            DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
            IsTemp: 0,
            IsUse: false
          }, {
            DrugCode: "Y00000000532",
            DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
            IsTemp: 0,
            IsUse: false
          },
            {
              DrugCode: "Y00000000667",
              DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
              IsTemp: 0,
              IsUse: false
            }, {
              DrugCode: "Y00000000537",
              DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
              IsTemp: 0,
              IsUse: false
            }]
        }, {
          Date: "2019-10-06",
          UserDefineDrugList: [{
            DrugCode: "Y00000000668",
            DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
            IsTemp: 0,
            IsUse: false
          }, {
            DrugCode: "Y00000000532",
            DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
            IsTemp: 0,
            IsUse: true
          },
            {
              DrugCode: "Y00000000667",
              DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
              IsTemp: 0,
              IsUse: false
            }, {
              DrugCode: "Y00000000537",
              DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
              IsTemp: 0,
              IsUse: true
            }]
        }, {
          Date: "2019-10-07",
          UserDefineDrugList: [{
            DrugCode: "Y00000000668",
            DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
            IsTemp: 0,
            IsUse: false
          }, {
            DrugCode: "Y00000000532",
            DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
            IsTemp: 0,
            IsUse: true
          },
            {
              DrugCode: "Y00000000667",
              DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
              IsTemp: 0,
              IsUse: false
            }, {
              DrugCode: "Y00000000537",
              DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
              IsTemp: 0,
              IsUse: true
            }]
        }, {
          Date: "2019-10-08",
          UserDefineDrugList: [{
            DrugCode: "Y00000000668",
            DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
            IsTemp: 0,
            IsUse: false
          }, {
            DrugCode: "Y00000000532",
            DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
            IsTemp: 0,
            IsUse: true
          },
            {
              DrugCode: "Y00000000667",
              DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
              IsTemp: 0,
              IsUse: false
            }, {
              DrugCode: "Y00000000537",
              DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
              IsTemp: 0,
              IsUse: true
            }]
        }, {
          Date: "2019-10-09",
          UserDefineDrugList: [{
            DrugCode: "Y00000000668",
            DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
            IsTemp: 0,
            IsUse: false
          }, {
            DrugCode: "Y00000000532",
            DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
            IsTemp: 0,
            IsUse: false
          },
            {
              DrugCode: "Y00000000667",
              DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
              IsTemp: 0,
              IsUse: false
            }, {
              DrugCode: "Y00000000537",
              DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
              IsTemp: 0,
              IsUse: false
            }]
        }, {
          Date: "2019-10-10",
          UserDefineDrugList: [{
            DrugCode: "Y00000000668",
            DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
            IsTemp: 0,
            IsUse: true
          }, {
            DrugCode: "Y00000000532",
            DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
            IsTemp: 0,
            IsUse: true
          },
            {
              DrugCode: "Y00000000667",
              DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
              IsTemp: 0,
              IsUse: true
            }, {
              DrugCode: "Y00000000537",
              DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
              IsTemp: 0,
              IsUse: true
            }]
        }, {
          Date: "2019-10-11",
          UserDefineDrugList: [{
            DrugCode: "Y00000000668",
            DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
            IsTemp: 0,
            IsUse: true
          }, {
            DrugCode: "Y00000000532",
            DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
            IsTemp: 0,
            IsUse: true
          },
            {
              DrugCode: "Y00000000667",
              DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
              IsTemp: 0,
              IsUse: true
            }, {
              DrugCode: "Y00000000537",
              DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
              IsTemp: 0,
              IsUse: true
            }]
        }, {
          Date: "2019-10-12",
          UserDefineDrugList: [{
            DrugCode: "Y00000000668",
            DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
            IsTemp: 0,
            IsUse: true
          }, {
            DrugCode: "Y00000000532",
            DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
            IsTemp: 0,
            IsUse: true
          },
            {
              DrugCode: "Y00000000667",
              DrugInfo: "【长】08-29 11:07:59  10mg/QD/im  注射用胸腺五肽  （孔翔宇）",
              IsTemp: 0,
              IsUse: true
            }, {
              DrugCode: "Y00000000537",
              DrugInfo: "【长】10-07 16:07:59  2.5mg/ST/P.O  来曲唑片  （孔翔宇）",
              IsTemp: 0,
              IsUse: true
            }]
        }],
        /*自定义药品y轴数据循环*/
        YUserDefineDrugList: [
          {
          DrugName: "青霉素",
          DrugCode: "Y00000000668"
        }, {
          DrugName: "来曲唑片",
          DrugCode: "Y00000000532"
        },{
            DrugName: "葡萄糖",
            DrugCode: "Y00000000667"
          }, {
            DrugName: "阿莫西林",
            DrugCode: "Y00000000537"
          }],
        /*自定义项目检验结果项目*/
        UserDefineLabList: [],
        /*自定义项目检验结果项目Y轴*/
        YUserDefineLabList: [],


        //图表体温脉搏静态数据
        // newdaydates:'',
        // ISBTN:'',
        // //体温，脉搏，呼吸，出量，入量，血压数据
        // FixedGuardianshipChartInfoList:[],
        // //手术名称数组
        // YOprList:[],
        // //手术数据
        // OperationInfoList:[],
        // //药品名称数组
        // YAntibacterialDrugList:[],
        // //药品数据
        // AntibacterialDrugList: [],
        // //自定义项目检验结果名称数组
        // YUserDefineLabList:[],
        // //自定义项目检验结果数据
        // UserDefineLabList:[],
        //自定义项目药品名称数组
        // YUserDefineDrugList:[],
        // //自定义项目药品数据
        // UserDefineDrugList:[],
        // //病原学送检
        // PathogenicExaminationList:[],
        //住院天数Array
        // dayS:[1,2,3,4,5,6,7,8,9,10],


        //异常检验结果每行内容弹出框静态
        // ShowTestresult:false,
        // LabDetailList:[],//详情表格数据
        //
        // CaseId:'',
        // isInHospital:'',
        // IEndDate:'',

      }
    },
    methods: {
      drawLine(){
        // 基于准备好的dom，初始化echarts实例
        let myChart = this.$echarts.init(document.getElementById('myChart'));
        //处理数据赋值到echarts
        var dateArray=[];
        var twArray=[];
        var mbArray=[];
        for(var i=0;i<this.FixedGuardianshipChartInfoList.length;i++){
          dateArray.push(this.FixedGuardianshipChartInfoList[i].Date);
          twArray.push(this.FixedGuardianshipChartInfoList[i].Temperature);
          mbArray.push(this.FixedGuardianshipChartInfoList[i].Pulse);
        }
        // 绘制图表
        myChart.setOption({
          title: {
            text: '',
            x: 'center',
            align: 'right',
            textStyle:{
              color:'#000',
              fontSize:14,
              fontWeight:'bold',
            },
          },
          tooltip: {
            trigger: 'axis'
          },
          yAxis : [
            {
              name:'脉搏(次/分)',
              type: 'value',
              position:'left',
              offset:80,//y轴偏移
              min: 30,
              max: 150,
              interval: 10,
              axisLabel: {
                textStyle: {
                  color: '#1369a6'
                }
              },
              axisLine: {
                lineStyle: {
                  type: 'solid',
                  color:'#1369a6',
                  width:'1'
                }
              },
            },
            {
              name:'体温（℃）',
              type: 'value',
              min: 35.0,
              max: 41.0,
              interval:0.5 ,

              position:'left',//y轴位置
              axisLabel: {
                formatter: '           {value}',
                textStyle: {
                  color: 'red'
                }
              },
              axisLine: {
                lineStyle: {
                  type: 'solid',
                  color:'red',
                  width:'1'
                }
              },
            },
          ],
          legend: {
            show:true,
            data:['脉搏','体温'],
            left:"center"
          },
          grid: {
            left: '3%',
            right: '4%',
            bottom: '3%',
            containLabel: true
          },
          toolbox: {
            show: true, //是否显示
            orient: 'horizontal', //水平显示(vertical为垂直显示)
            x: '1533px', //距离X轴多远
            feature: {
              saveAsImage: {
                name:'体温脉搏图'
              }
            }
          },
          xAxis: {
            type: 'category',
            data: dateArray,
            axisLabel:{//间隔
              interval:0,
            }
          },
          series: [{
            name:"体温",
            data: twArray,
            type: 'line',
            yAxisIndex:1,//数据对应y轴
            lineStyle: {
              type: 'solid',
              color:'red',
              width:'1'
            }
          },
            {
              name:"脉搏",
              data: mbArray,
              type: 'line',
              yAxisIndex:0,//数据对应y轴
              lineStyle: {
                type: 'solid',
                color:'#1369a6',
                width:'1'
              }
            }
          ]
        })
      },
      //第一次进入页面表格传递时间数据获取十天//获取图表数据函数
      // echartsCreated(){
      //
      //   const loading= this.$loading({//加载中loading
      //     lock: true,
      //     text: '努力加载中',
      //     spinner: 'el-icon-loading',
      //     background: 'rgba(250,250,250,1)',
      //     target: document.querySelector('#lodingIdTable')
      //   });//loading.close();//关闭加载中loading
      //   // 获取入院时间时间格式的时间戳
      //   var stringTime = this.$route.params.StartDate;
      //
      //   var now = new Date(stringTime);
      //   //时间戳转为字符串格式
      //   var year = now.getFullYear();
      //   var month = now.getMonth() + 1;
      //   var date = now.getDate();
      //   if (month >= 0 && month <= 9) {
      //     month = "0" + month;
      //   }
      //   if (date >= 0 && date <= 9) {
      //     date = "0" + date;
      //   }
      //   var oneDay = year + "-" + month + "-" + date;//当前开头第一天日期传回后台
      //   var IsInhospIS=this.isInHospital;//判断一下布尔
      //   this.$axios({
      //     method:'get',
      //     url:window.apiUrl+'/pc/patguardianshipchart/GetContinueFixedGuardianshipChart',
      //     params: {
      //       CaseId:this.CaseId,
      //       PatType:IsInhospIS,
      //       IEndDate:this.IEndDate,
      //       StartDate:oneDay,
      //       TotalDays:10
      //     },
      //   }).then(res => {
      //     if(res.data.Errs.length==0){
      //       let echartsdata=res.data.Result.FixedGuardianshipChartInfoList;//拿到数据处理渲染图表echarts
      //       this.FixedGuardianshipChartInfoList=res.data.Result.FixedGuardianshipChartInfoList;
      //       this.YOprList=res.data.Result.YOprList;//放出手术信息即可
      //       this.OperationInfoList=res.data.Result.OperationInfoList;//放出手术信息即可
      //       this.YAntibacterialDrugList=res.data.Result.YAntibacterialDrugList;//放出药品信息即可
      //       this.AntibacterialDrugList=res.data.Result.AntibacterialDrugList;//放出药品信息即可
      //       this.PathogenicExaminationList=res.data.Result.PathogenicExaminationList;//病原学送检数据
      //       var ISBTN='';
      //       for(var i=0;i<echartsdata.length;i++){
      //         ISBTN=echartsdata[0].Date
      //       };
      //       this.drawLine();//调用echarts函数
      //       this.ISBTN=ISBTN;
      //     }else{
      //       var Errs=res.data.Errs;
      //       var errs2=Errs[0];
      //       this.$message({
      //         type: "error",
      //         message: errs2
      //       });
      //     }
      //   }).catch(err => { //请求失败就会捕获报错信息
      //     //err.response可拿到服务器返回的报错数据
      //     //console.log(res.data.errs)
      //   });
      //
      //   //调用自定义项目接口并赋值
      //   this.$axios({
      //     method:'get',
      //     url:window.apiUrl+'/pc/patguardianshipchart/GetContinueUserDefineGuardianshipChart',
      //     params: {
      //       CaseId:this.CaseId,
      //       PatType:IsInhospIS,
      //       IEndDate:this.IEndDate,
      //       StartDate:oneDay,
      //       TotalDays:10
      //     },
      //   }).then(res => {
      //     //console.log(res)//拿到数据处理渲染图表echarts
      //     this.YUserDefineLabList=res.data.Result.YUserDefineLabList;//放出检验结果信息即可
      //     this.UserDefineLabList=res.data.Result.UserDefineLabList;//放出检验结果信息即可
      //     this.YUserDefineDrugList=res.data.Result.YUserDefineDrugList;//自定义药品
      //     this.UserDefineDrugList=res.data.Result.UserDefineDrugList;//自定义药品
      //     loading.close();//关闭加载中loading
      //   }).catch(err => { //请求失败就会捕获报错信息
      //     //err.response可拿到服务器返回的报错数据
      //     //console.log(res.data.errs)
      //   });
      // },
    },
    mounted(){
      this.drawLine();//调用echarts函数
      /*调用*/
      // this.echartsCreated()
    },
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


  .borderLeft{
    border-left: 5px solid #1369a6;
    padding-left: 20px;
  }

  .btnfive{
    border: solid 1px #dcdfe6;
    border-radius: 4px;
    height: 22px;
    line-height: 22px;
    display: inline-block;
    width: 50px;
    text-align: center;
    font-weight: initial!important;
    cursor: pointer;
    color: #666666;
  }
  /*手术*/
  .iconcolor{
    display: inline-block;
    width: 20px;
    height: 20px;
    margin-top: 4px;
    position:relative;
    z-index:2;
    /*background-color: pink;*/
  }
  .iconcolor:hover{
    z-index:3;
    /*background:none;*/
  }
  .iconcolor .tdtip  {
    display: none;
  }
  .iconcolor:hover .tdtip  {
    display: block;
    width: 400px;
    max-height: 80px;
    overflow-y: auto;
    position: absolute;
    top: 8px;
    border-radius: 20px;
    /*hover背景色*/
    background-color:  #1369a6;
    opacity:0.8;
    color: #ffffff;
    /*word-break: break-all;*/
  }


  /*病原学送检*/
  .PEiconcolor{
    display: inline-block;
    width: 20px;
    height: 20px;
    margin-top: 4px;
    position:relative;
    z-index:2;
    /*background-color: pink;*/
  }
  .PEiconcolor:hover{
    z-index:3;
    /*background:none;*/
  }
  .PEiconcolor .PEtdtip  {
    display: none;
  }
  .PEiconcolor:hover .PEtdtip  {
    display: block;
    width: 400px;
    max-height: 80px;
    overflow-y: auto;
    position: absolute;
    top: 8px;
    border-radius: 20px;
    /*hover背景色*/
    background-color:  #1369a6;
    opacity:0.8;
    color: #ffffff;
    /*word-break: break-all;*/
  }


  .ADDbackground{
    background-color:  #1369a6;
    color: #ffffff;
    border: solid 1px #1369a6!important;
  }


  /*药品*/
  .Drugiconcolor{
    display: inline-block;
    width: 100%;
    height: 10px;
    margin-top: 4px;
    position:relative;
    z-index:2;
    background-color: #1369a6;
  }
  .Drugiconcolor:hover{
    z-index:3;
    /*background:none;*/
  }
  .Drugiconcolor .Drugtdtip  {
    display: none;
  }
  .Drugiconcolor:hover .Drugtdtip  {
    display: block;
    width: 400px;
    max-height: 80px;
    overflow-y: auto;
    border-radius: 20px;
    position: absolute;
    top: 8px;
    /*hover背景色*/
    background-color: #1369a6;
    opacity:0.8;
    color: #ffffff;
    word-break: break-all;
  }



  .specialheader{
    /*border-left: 5px solid #136aa7;*/
    height: 28px;
    line-height: 28px;
  }
  .specialheader>span{
    font-size: 14px;
    font-weight: bold;
    margin-left: 20px;
  }

  #infotableid,#infotableid tr th, #infotableid tr td {
    border:1px solid #e5e5e5;
  }
  #infotableid {
    width: 1568px;
    min-height: 25px;
    line-height: 25px;
    text-align: center;
    border-collapse: collapse;
    /*padding:2px;*/
    margin-left: -1px;
  }
  /*特殊提示*/
  #thereinfo{
    display: flex;
    margin-top: 10px;
  }
  .ADRinfo{
    /*border: 1px solid red;*/
    min-width: 300px;
    height: 200px;
    background-color: #ffffff;
    box-shadow: 2px 4px 30px 6px
    rgba(219, 225, 231, 0.8);
    border-radius: 6px;
    margin-right: 8px;
    margin-bottom: 8px;
    /*float: left;*/
    cursor: pointer;
    padding: 10px;
    padding-left: 15px;
    padding-right: 15px;
    padding-top: 15px;
    /*flex: 1;*/
  }
  .ADRinfo>p{
    margin-bottom: 15px;
  }
  .LabPromptListBox{
    padding: 10px;
    width: 300px;
    height: 200px;
    background-color: #ffffff;
    box-shadow: 2px 4px 30px 6px
    rgba(219, 225, 231, 0.8);
    border-radius: 6px;
    margin-right: 8px;
    margin-bottom: 8px;
    /*float: left;*/
    cursor: pointer;
  }
  .PASSBox{
    width: 300px;
    height: 200px;
    background-color: #ffffff;
    box-shadow: 2px 4px 30px 6px
    rgba(219, 225, 231, 0.8);
    border-radius: 6px;
    margin-right: 8px;
    margin-bottom: 8px;
    /* float: left; */
    cursor: pointer;
    padding: 10px;
  }



  /*弹出框*/
  .modalshow{
    width: 100%;
    height: 100%;
    z-index: 30;
    background-color: rgba(0,0,0,0.8);
    position: fixed;
    top:0;
    left: 0;
    right: 0;
    bottom: 0;

  }
  .modalsize{
    padding: 50px;
    width: 1100px;
    height: 300px;
    background-color: #ffffff;
    overflow-y: auto;
    margin: auto;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }
  .modalsizexz{
    padding: 50px;
    width: 580px;
    height: 400px;
    background-color: #ffffff;
    overflow-y: auto;
    margin: auto;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }
  .btnbox{
    text-align: right;
    margin-top: 25px;
  }
  .btnboxxz{
    text-align: center;
    margin-top: 50px;
  }

  .outdel{
    display: inline-block;
  }
  .adddel{
    display: inline-block;
    margin-left: 20px;
  }
  /*#modalshow{*/
  /*z-index: 1000!important;*/
  /*}*/
  /*监护图表*/
  .jhtable{
    width: 100%;
    /*height: 500px;*/
    /*border: 1px solid #ebeef5;*/
  }
  .jhtbsx{
    /*padding-left: 20px;*/
  }
  .jhtbsx>p{
    margin-top: 10px;
  }
  .titlecustom{
    background-color: #ecf5ff;
    width: 100%;
    height: 40px;
    line-height: 40px;
    color: #000000;
    font-weight: bold;
    font-size: 16px;
    position: relative;
    /*margin-bottom: 5px;*/
  }
  .titlecustom span{
    display: inline-block;
    /*margin-left: 20px;*/
  }
  /*s手术背景图片*/
  .OperationBacImg{
    /*background-image: url('../../../../static/PC/img/lampIcon/OperationIcon.png');*/
    /*background-color: none;*/
  }

  #TestresultChart{
    width: 900px;
    height: 300px;
  }
  .Testresultoutdelbtnclass{
    text-align: center;
    margin-top: 30px;
    /*position: absolute;*/
    /*bottom: 0px;*/
  }
</style>
