# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил(а):
- Уткин Никита Александрович
- РИ231113
- 
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)


## Цель работы
Познакомиться с одной из первых моделей нейросетей - перцептроном и реализовать эту модель в Unity

## Задание 1. В проекте Unity реализовать перцептрон, который умеет производить вычисления

Создали пустой объект и подкрутили код:

```py
﻿using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
	public double[] input;
	public double output;
}

public class Perceptron : MonoBehaviour {

	public TrainingSet[] ts;
	double[] weights = {0,0};
	double bias = 0;
	double totalError = 0;

	double DotProductBias(double[] v1, double[] v2) 
	{
		if (v1 == null || v2 == null)
			return -1;
	 
		if (v1.Length != v2.Length)
			return -1;
	 
		double d = 0;
		for (int x = 0; x < v1.Length; x++)
		{
			d += v1[x] * v2[x];
		}

		d += bias;
	 
		return d;
	}

	double CalcOutput(int i)
	{
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}

	void InitialiseWeights()
	{
		for(int i = 0; i < weights.Length; i++)
		{
			weights[i] = Random.Range(-1.0f,1.0f);
		}
		bias = Random.Range(-1.0f,1.0f);
	}

	void UpdateWeights(int j)
	{
		double error = ts[j].output - CalcOutput(j);
		totalError += Mathf.Abs((float)error);
		for(int i = 0; i < weights.Length; i++)
		{			
			weights[i] = weights[i] + error*ts[j].input[i]; 
		}
		bias += error;
	}

	double CalcOutput(double i1, double i2)
	{
		double[] inp = new double[] {i1, i2};
		double dp = DotProductBias(weights,inp);
		if(dp > 0) return(1);
		return (0);
	}

	void Train(int epochs)
	{
		InitialiseWeights();
		
		for(int e = 0; e < epochs; e++)
		{
			totalError = 0;
			for(int t = 0; t < ts.Length; t++)
			{
				UpdateWeights(t);
				Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
			}
			Debug.Log("TOTAL ERROR: " + totalError);
		}
	}

	void Start () {
		Train(8);
		Debug.Log("Test 0 0: " + CalcOutput(0,0));
		Debug.Log("Test 0 1: " + CalcOutput(0,1));
		Debug.Log("Test 1 0: " + CalcOutput(1,0));
		Debug.Log("Test 1 1: " + CalcOutput(1,1));		
	}
	
	void Update () {
		
	}
}
```

Оттестировать на OR, AND, NAND и XOR работу перцептрона:

1) OR - **Работает**. Чтобы работал без ошибок нужно 3 итерации(эпохи)

2) AND - **Работает**. Чтобы работал без ошибок нужно 3 итерации(эпохи)

3) NAND - **Работает**. Чтобы работал без ошибок нужно 3 итерации(эпохи)

4) XOR - Для него не работает т.к. функция исключающего ИЛИ - нелинейная, а перцептрон работает только с линейными функциями

## Задание 2. Построить графики зависимости количества эпох от ошибки обучения. Указать от чего зависит необходимое количество эпох обучения
![image](https://github.com/user-attachments/assets/7a687740-3379-495d-9358-2a49d298af9a)

![image](https://github.com/user-attachments/assets/daa46c40-9d37-4c19-a8ef-1a29e8fee724)

![image](https://github.com/user-attachments/assets/4cfdd765-ec72-402c-846f-1601f8287134)

![image](https://github.com/user-attachments/assets/753deb85-eee3-4cd3-b40b-80e9a640a05b)

https://docs.google.com/spreadsheets/d/1cx6HeyF1VQ6EziiOmGr9jyp4ZV1ingmPMM-r7eTvIEc/edit?usp=sharing

## Задание 3. Построить визуальную модель работы перцептрона на сцене Unity

  unitypackage
  
## Выводы

Ознакомился с перцептроном, на теории, на практике, что он может и исследовал некоторые функцции для него

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
