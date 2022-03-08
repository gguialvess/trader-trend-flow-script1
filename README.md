# trader-trend-flow-script1
trader trend flow script

instrument {
    name = 'INSTAGRAM:CRACKTRADINGACADEMY_OFICIAL',
    short_name = 'INSTAGRAM:CRACKTRADINGACADEMY_OFICIAL',
  
    overlay =true
}

MaFast_period = input(1,"Ma Fast period",input.integer,1,1000,1)
MaValue = input(5,"Ma Value", input.string_selection,inputs.titles)

MaSlow_period = input(34,"Ma Slow period",input.integer,1,1000,1)

Signal_period = input(4,"Signal period",input.integer,1,1000,1)

input_group {
    "Compra",
    colorBuy = input { default = "blue", type = input.color }, 
    visibleBuy = input { default = true, type = input.plot_visibility }
}

input_group {
    "Venda",
    colorSell = input { default = "yellow", type = input.color },
    visibleSell = input { default = true, type = input.plot_visibility }
}

local titleValue = inputs[MaValue]

-- mdia mvel linear rpida
smaFast = sma(titleValue, MaFast_period)

-- mdia mvel linear devagar
smaSlow = sma(titleValue, MaSlow_period)

-- calculo diferencial - serie
buffer1 = smaFast - smaSlow 

-- clculo da mdia mvel ponderada - serie
buffer2 = wma(buffer1, Signal_period)

buyCondition = conditional(buffer1 > buffer2 and buffer1[1] < buffer2[1] and not (buffer1 < buffer2 and buffer1[1] > buffer2[1]))
buyCondition = conditional(buffer1 > buffer2 and buffer1[1] < buffer2[1])

sellCondition = conditional(buffer1 < buffer2 and buffer1[1] > buffer2[1] and not (buffer1 > buffer2 and buffer1[1] < buffer2[1]))
sellCondition = conditional(buffer1 < buffer2 and buffer1[1] > buffer2[1] )

            plot_shape(
                (buyCondition),
                "30",
                shape_style.arrowup,
                shape_size.large,
                colorBuy,
                shape_location.belowbar,
                -1,
                "CRACK TRADING ACADEMY",
                "blue"
               ) 

          plot_shape(
              (sellCondition),
                "30",
                shape_style.arrowdown,
                shape_size.large,
                colorSell,
                shape_location.abovebar,
                -1,
                "CRACK TRADING ACADEMY",
                "YELLOW"
          )
instrument{name="AXX SUPORT/RES SETAS",icon='https://www.google.com/url?sa=i&url=https%3A%2F%2Fmyicons.co%2F&psig=AOvVaw3UTgfDo_l_YxT4qVtiaoE7&ust=1638095965421000&source=images&cd=vfe&ved=0CAsQjRxqFwoTCKCli5WtuPQCFQAAAAAdAAAAABAD',overlay=true}

local function a()local 
b=make_series()local c=high[2]

if not get_value(c)then 
return b end;
local d=high<=c and high[1]<=c and high[3]<=c and high[4]<=c;
b:set(iff(d,c,b[1]))return b end;
local function e()local b=make_series()local c=low[2]if not get_value(c)then return b end;
local d=low>=c and low[1]>=c and low[3]>=c and low[4]>=c;
b:set(iff(d,c,b[1]))return b end;
input_group{"Color",color=input{default="LIME",type=input.color},width=input{default=1,type=input.line_width}}h=a()l=e()hline(h,"High",color,high_width)hline(l,"Low",color,width)hline(highest(10)[1],"HH10",color,1)hline(lowest(10)[1],"LL10",color,1)hline(highest(30)[1],"HH30",color,1)hline(lowest(30)[1],"LL30",color,1)hline(highest(60)[1],"HH60",color,1)hline(lowest(60)[1],"LL60",color,1)hline(highest(100)[1],"HH100",color,1)hline(lowest(100)[1],"LL100",color,1)hline(highest(150)[1],"HH150",color,1)hline(lowest(150)[1],"LL150",color,1)hline(highest(200)[1],"HH200",color,1)hline(lowest(200)[1],"LL200",color,1)
instrument {
    name = 'AXX TREND PERFECT',
    short_name = 'SMA-ENG',
    icon = 'indicators:BB',
    overlay = true
}


MaFast_period = input(3,"Ma Fast period",input.integer,1,1000,1)
MaFast_average = input(4,"Ma Fast average", input.string_selection,averages.titles)
MaFast_title = input(1,"Ma Fast title", input.string_selection,inputs.titles)

MaSlow_period = input(7,"Ma Slow period",input.integer,1,1000,1)
MaSlow_average = input(2,"Ma Slow average", input.string_selection,averages.titles)
MaSlow_title = input(1,"Ma Slow title", input.string_selection,inputs.titles)

MaTrend_period = input(100,"Ma Trend period",input.integer,1,1000,5)
MaTrend_average = input(2,"Ma Trend average", input.string_selection,averages.titles)
MaTrend_title = input(1,"Ma Trend title", input.string_selection,inputs.titles)


input_group {
    "Area Up and Down",
    colorAreaUp = input { default = "rgba(34, 139, 34, 0.3)", type = input.color },  
    colorAreaDown = input { default = "rgba(220, 20, 60, 0.3)", type = input.color },
    visibleArea = input { default = true, type = input.plot_visibility } 
}


input_group {
    "Ma Slow Line",
    colorSlow = input { default = "purple", type = input.color },
    widthSlow = input { default = 2, type = input.line_width},
    visibleSlow = input { default = true, type = input.plot_visibility }
}



input_group {
    "Buy Outside Bar",
    colorBuy2 = input { default = "lime", type = input.color }, 
    visibleBuy2 = input { default = true, type = input.plot_visibility }
}

input_group {
    "Sell Outside Bar",
    colorSell2 = input { default = "red", type = input.color },
    visibleSell2 = input { default = true, type = input.plot_visibility }
}

local avgFast = averages[MaFast_average]
local titleFast = inputs[MaFast_title]

local avgSlow = averages[MaSlow_average]
local titleSlow = inputs[MaSlow_title]

local avgTrend = averages[MaTrend_average]
local titleTrend = inputs[MaTrend_title]

if visibleFast == true then
    plot(avgFast(titleFast,MaFast_period),"Ma Fast",colorFast,widthFast)
end

if visibleSlow == true then
    plot(avgSlow(titleSlow,MaSlow_period),"Ma Slow",colorSlow,widthSlow)
end

if visibleTrend == true then
    plot(avgTrend(titleTrend,MaTrend_period),"Ma Trend",colorTrend,widthTrend)
end

candle_time = {"1s", "5s", "10s", "15s", "30s", "1m", "2m", "5m", "10m", "15m", "30m", "1H", "2H", "4H", "8H", "12H", "1D", "1W", "1M", "1Y"}
candle_time_res = input(6,"Candle check resolution",input.string_selection,candle_time)

sec = security (current_ticker_id, candle_time[candle_time_res])

filter_source = {"1s", "5s", "10s", "15s", "30s", "1m", "2m", "5m", "10m", "15m", "30m", "1H", "2H", "4H", "8H", "12H", "1D", "1W", "1M", "1Y"}
filter_pa_index = input(8,"Candle check resolution",input.string_selection,filter_source)

filter_pa = security (current_ticker_id, filter_source[filter_pa_index])

--print(filter_source[filter_pa_index])

if (sec ~= nil) then
    
    MaFast0 = avgFast(titleFast,MaFast_period) --Ma Fast bar 0
    MaFast1 = MaFast0[1]                       --Ma Fast bar 1
    
    MaSlow0 = avgSlow(titleSlow,MaSlow_period) --Ma Slow bar 0
    MaSlow1 = MaSlow0[1]
    
    MaTrend0 = avgTrend(titleTrend,MaTrend_period)
    MaTrend1 = MaTrend0[1]
    
    if(invsibleBuy == true) then
        plot_shape((close > open and close[1] < open[1] and close > MaFast0 and MaFast0 > MaSlow0 and MaSlow0 > MaTrend0 and close > open[1] and open <= close[1] and abs(close-open) > abs(close[1]-open[1])),
            "Call",
            shape_style.triangleup,
            shape_size.huge,
            colorBuy,
            shape_location.belowbar,
            0,
            "TOURO",
            colorBuy  
           ) 
    end
    
    if (invisibleSell == true) then
        plot_shape((close < open and close[1] > open[1] and close < MaFast0 and MaFast0 < MaSlow0 and MaSlow0 < MaTrend0 and close < open[1] and open >= close[1] and abs(close-open) > abs(close[1]-open[1])),
            "Put",
            shape_style.triangledown,
            shape_size.huge,
            colorSell,
            shape_location.abovebar,
            0,
            "URSO",
            colorSell
        )
    end


    if(invisibleBuy1 == true) then 
        if(filter_pa.close[1] > filter_pa.open[1] and filter_pa.close[2] < filter_pa.open[2] and filter_pa.close[1] > filter_pa.open[2] and filter_pa.open[1] <= filter_pa.close[2] and abs(filter_pa.close[1]-filter_pa.open[1]) > abs(filter_pa.close[2]-filter_pa.open[2]) ) then                                 
            plot_shape((close > open and close[1] < open[1] and close > open[1] and open <= close[1] and abs(close-open) > abs(close[1]-open[1])),
                "Call1",
                shape_style.triangleup,
                shape_size.huge,
                colorBuy1,
                shape_location.belowbar,
                0,
                "TOURO",
                colorBuy1  
               ) 
    end
    end
    
    if (invisibleSell1 == true) then
        if(filter_pa.close[1] < filter_pa.open[1] and filter_pa.close[2] > filter_pa.open[2] and filter_pa.close[1] < filter_pa.open[2] and filter_pa.open[1] >= filter_pa.close[2] and abs(filter_pa.close[1]-filter_pa.open[1]) > abs(filter_pa.close[2]-filter_pa.open[2]) ) then                                 
            plot_shape((close < open and close[1] > open[1] and close < open[1] and open >= close[1] and abs(close-open) > abs(close[1]-open[1])),
                "Put1",
                shape_style.triangledown,
                shape_size.huge,
                colorSell1,
                shape_location.abovebar,
                0,
                "URSO",
                colorSell1
            )
        end
    end


     if(invisibleBuy2 == true) then 
        --if(filter_pa.close[1] > filter_pa.open[1] and filter_pa.close[2] < filter_pa.open[2] and filter_pa.close[1] > filter_pa.open[2] and filter_pa.open[1] <= filter_pa.close[2] and abs(filter_pa.close[1]-filter_pa.open[1]) > abs(filter_pa.close[2]-filter_pa.open[2]) ) then                                 
            plot_shape((open[3] < close[3] and open[2] < close[2] and open[1] > close[1] and close[1] > open[2] and open[1] > open[2] and open < close),
                "SNIPER-CALL2",
                shape_style.triangleup,
                shape_size.huge,
                colorBuy2,
                shape_location.belowbar,
                0,
                "TOURO",
                colorBuy2  
               ) 
    --end
    end

    if (invisibleSell2 == true) then
        --if(filter_pa.close[1] < filter_pa.open[1] and filter_pa.close[2] > filter_pa.open[2] and filter_pa.close[1] < filter_pa.open[2] and filter_pa.open[1] >= filter_pa.close[2] and abs(filter_pa.close[1]-filter_pa.open[1]) > abs(filter_pa.close[2]-filter_pa.open[2]) ) then                                 
           plot_shape((open[3] > close[3] and open[2] > close[2] and open[1] < close[1] and close[1] < open[2] and open[1] < open[2] and open > close),
                "SNIPER-PUT2",
                shape_style.triangledown,
                shape_size.huge,
                colorSell2,
                shape_location.abovebar,
                0,
                "URSO",
                colorSell2
            )
        --end
    end




    if (visibleArea == true) then
        fill(MaFast0,MaSlow0,"Area", MaFast0 > MaSlow0 and colorAreaUp or MaFast0 < MaSlow0 and colorAreaDown )
    
   end


end

MaFast_period = input(3,"Ma Fast period",input.integer,1,1000,1)
MaFast_average = input(4,"Ma Fast average", input.string_selection,averages.titles)
MaFast_title = input(1,"Ma Fast title", input.string_selection,inputs.titles)

MaSlow_period = input(7,"Ma Slow period",input.integer,1,1000,1)
MaSlow_average = input(2,"Ma Slow average", input.string_selection,averages.titles)
MaSlow_title = input(1,"Ma Slow title", input.string_selection,inputs.titles)

MaTrend_period = input(200,"Ma Trend period",input.integer,1,1000,5)
MaTrend_average = input(2,"Ma Trend average", input.string_selection,averages.titles)
MaTrend_title = input(1,"Ma Trend title", input.string_selection,inputs.titles)
 

 
input_group {
    "Buy Arrow",
    colorBuy = input { default = "lime", type = input.color },
    visibleBuy = input { default = true, type = input.plot_visibility }
}

input_group {
    "Sell Arrow",
    colorSell = input { default = "red", type = input.color },
    visibleSell = input { default = true, type = input.plot_visibility }
}

local avgFast = averages[MaFast_average]
local titleFast = inputs[MaFast_title]

local avgSlow = averages[MaSlow_average]
local titleSlow = inputs[MaSlow_title]

local avgTrend = averages[MaTrend_average]
local titleTrend = inputs[MaTrend_title]

if visibleFast == true then
    plot(avgFast(titleFast,MaFast_period),"Ma Fast",colorFast,widthFast)
end

if visibleSlow == true then
    plot(avgSlow(titleSlow,MaSlow_period),"Ma Slow",colorSlow,widthSlow)
end

if visibleTrend == true then
    plot(avgTrend(titleTrend,MaTrend_period),"Ma Trend",colorTrend,widthTrend)
end

candle_time = {"1s", "5s", "10s", "15s", "30s", "1m", "2m", "5m", "10m", "15m", "30m", "1H", "2H", "4H", "8H", "12H", "1D", "1W", "1M", "1Y"}
candle_time_res = input(6,"Candle check resolution",input.string_selection,candle_time)

sec = security (current_ticker_id, candle_time[candle_time_res])

if (sec ~= nil) and (sec.open_time == open_time) then
    
    Mafast0 = avgFast(titleFast,MaFast_period) --Ma Fast bar 0
    Mafast1 = Mafast0[1]                       --Ma Fast bar 1
    
    MaSlow0 = avgSlow(titleSlow,MaSlow_period) --Ma Slow bar 0
    MaSlow1 = MaSlow0[1]
    
    MaTrend0 = avgTrend(titleTrend,MaTrend_period)
    Matrend1 = MaTrend0[1]
    
    plot_shape((close > open and close[1] < open[1] and close > Mafast0 and close > MaSlow0 and close > MaTrend0 and close > open[1] and open <= close[1] and abs(close-open) > abs(close[1]-open[1])),
        "CALL",
        shape_style.triangleup,
        shape_size.tiny,
        colorBuy,
        shape_location.belowbar,
        0,
        "",
        colorBuy  
       ) 
    
    plot_shape((close < open and close[1] > open[1] and close < Mafast0 and close < MaSlow0 and close < MaTrend0 and close < open[1] and open >= close[1] and abs(close-open) > abs(close[1]-open[1])),
        "PUT",
        shape_style.triangledown,
        shape_size.tiny,
        colorSell,
        shape_location.abovebar,
        0,
        "",
        colorSell
    )
    


end
