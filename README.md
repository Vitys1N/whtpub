#!/bin/bash
#быки и коровы
list=("1" "2" "3" "4" "5" "6" "7" "8" "9")
list=($(shuf -e "${list[@]}"))
numbii="${list[0]}""${list[1]}""${list[2]}""${list[3]}" #создание числа
numbh=(0 0 0 0) 
cnt=1 
while [ $cnt -ne 2 ]
do
echo Введите число без повторяющихся цифр
read a; 
if [[ $a = *[0-9]* ]]; #это действителтно число
then 
  if [ ${#a} = ${#numbii} ]; #4 знака числа
  then 
    for i in {3..0} #загоняем цифры по одной в число
    do
      numbh2=$(($a % 10))
      numbh[$i]=$numbh2
      a=$(($a / 10))
    done
    numbf="${numbh[0]}""${numbh[1]}""${numbh[2]}""${numbh[3]}" #число для сравнения
    #если цифры в числе не различны
    if ([ ${numbh[0]} != ${numbh[1]} ]) && ([ ${numbh[0]} != ${numbh[2]} ]) && ([ ${numbh[0]} != ${numbh[3]} ]) && ([ ${numbh[1]} != ${numbh[2]} ]) && ([ ${numbh[1]} != ${numbh[3]} ]) && ([ ${numbh[2]} != ${numbh[3]} ]);
    then
      if [ $numbf = $numbii ];then #угадал число
      echo Победа
      cnt=2
      else
        bull=0 
        for i in {0..3} #перебор быков
        do
          if [ ${numbh[$i]} = ${list[$i]} ]; #цифра совпала/нет
          then 
          bull=$(($bull + 1)) 
          fi
        done
        echo $bull быков
        cow=0
        for i in {0..3} #перебор коров
        do
          for b in {0..3}
          do
            if [ ${numbh[$i]} = ${list[$b]} ]; #есть такая цифра/нет
            then 
            cow=$(($cow + 1))
            fi
          done
        done
        cow=$(($cow - $bull))
        echo $cow коров
      fi
    fi
  fi
fi
done
