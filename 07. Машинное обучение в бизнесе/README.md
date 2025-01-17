# Выбор локации для скважины
#### Описание исследования  
Целью исследования является построение модели для нефтедобывающей компании «ГлавРосГосНефть», 
которые будут применяться вычисления региона для добычи нефти, где деятельность компании принесёт наибольшую прибыль.  
   


Для проведения исследования были предоставлены три таблицы данных геологоразведки трёх регионов со следующими признаками:   
    - идентификатор скважины 
    - f0, f1, f2 — три признака точек добычи  
    - объём запасов в скважине
      
    
В работе мной были произведены следующие действия:  

1) Изучение общей информации:  
    - Изученеие файлов с данными, получение общей информации из файлов geo_data_0.csv, geo_data_1.csv, geo_data_2.csv      
2) Обучение и проверка модели для каждого региона:    
    - деление данных на обучающую и валидационную    
    - обучение модели линейной регрессии, составление предсказания на валидационной выборке    
    - вычисление среднего запаса предсказанного сырья и RMSE модели    
3) Рассчёт прибыли:    
    - рассчёт достаточного объёма сырья для безубыточной разработки новой скважины
4) Создание функции для расчёта прибыли по выбранным скважинам и предсказаниям модели:  
    - выбор 200 скважин с максимальными значениями предсказаний объёмов сырья   
    - суммирование целевых значений объёма сырья  
    - рассчёт прибыли для полученного объёма сырья
5) Рассчёт рисков и прибыли для каждого региона:    
    - нахождение прибыли с помощью Bootstrap
    - вычисление средней прибыли, 95%-й доверительного интервала и риска убытков  
    - формирование предложения для разработки скважины       
6) Оформление выводов.  
### Вывод   

В данной работе была поставлена задача с помощью модели линейной регрессии проанализировать добычу сырья в трёх регионах с целью выявления региона наиболее выгодного для инвестиций в разработку скважин.  
В ходе работы мной были произведены следующие действия:  
1) Изучение общей информации:  
Были полученны данные из файлов geo_data_0.csv, geo_data_1.csv, geo_data_2.csv.     
Данные соответствуют описанию в техническом задании.      
Дубликаты и пропуски обнаружены не были. Количество записей в каждой из таблиц: 10000       
Были построены распределения значений в таблицах по регионам.       
Нормальной распределение имеют следующие параметры:    
    Регион 1: f2    
    Регион 2: f1   
    Регион 3: f0, f1, f2    
Остальные параметры в таблицах имеют не нормальное распределение.  
Также у параметром f0, f1, f2 наблюдаются выбросы по графику boxplot.   
Так как нам неизвестна природа этих параметров, мы не можем оценить, насколько адекватно наличие подобных выбросов.       
При рассмотрении таблицы корреляции видим, что:  
    Регион 1: с целевым признаком коррелирует признак f2 (0.48), у признаков f1 и f0 обратная корреляция (-0.44)     
    Регион 2: признак f2 коллинеарен целевому признаку     
    Регион 3: признак f2 коррелирует с целевым признаком (0.45)      
        
2) Обучение и проверка модели для каждого региона:     
При оценке работы модели и полученных с её помощью предсказанных значений средних запасов сырья помним, 
что чем ближе метрика RMSE к нулю, тем точнее предсказание она делает.  
Рассматрвиая результаты работы модели, видим, что:  
    - В регионах 1 и 3 были предсказаны самые высокие показатели запасов сырья - 92.6 и 95 тыс. баррелей соответственно. 
    Однако метрики RMSE также высоки, что отражает неоднозначность предсказания, неточность модели  
    - В регионе 2 был предсказан запас сырья в 68.7  тыс. баррелей, при близкой к нулю метрике RMSE (0.89), что отражает точность работы модели  

3) Рассчёт прибыли:    
Достаточный объём продукта для безубыточной разработки составляет 111.11 тыс. баррелей.    
Данный показатель был рассчитан для 200 лучших скважин из выборки в 500 скважин.    
Замечаем, что предсказанный средний объём сырья со всех скважен в рассматриваемых регионах меньше, чем достаточный объём для безубыточного производства.  
4) Создание функции для расчёта прибыли по выбранным скважинам и предсказаниям модели:  
При подсчёте прибыли от 200 лучших скважин по предсказанным значениям выяснили, что:  
    - все 200 скважин преодолевают порог добычи в 111.11 тыс баррелей для безубыточного производства, больше всего у первого региона (155.5 тыс. баррелей)  
    - в первом регионе самы большой суммарный целевой объём сырья 31102.33 тыс. баррелей  
    - прибыль с полученного объёма сырья самая большая у первого региона: 3996.05 млн.руб
5) Рассчёт рисков и прибыли для каждого региона:    
На данном этапе были составлены функции для расчёта прибыли от добычи на скважинах в трёх регионах и для просчёта риска убытков.  
Было выявлены следующие наблюдения:  
- второй регион принесёт нибольшую среднюю выручку  
- второй регион имеет самый низкий риск убытков : ниже 2.5%  
- второй регион имеет самый узкий разброс по доверительному интервалу  
Таким образом при выборе региона для разработки скважин наименее рискованно и наиболее предсказуемо прорабатываеть вариант второго региона.       
  
