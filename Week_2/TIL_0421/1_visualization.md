## 시각화 

### 시각화 라이브러리 

여러 기법을 통해 스크래핑을 진행


### 꺾은선 그래프 (Line Plot)
```python
import seaborn as sns
sns.lineplot(x = x_list, y = y_list)
```
### 막대 그래프 (Bar Plot)
```python
import seaborn as sns
sns.barplot(x = x_list, y = y_list)
plt.title("Bar Pliot")      # 그래프에 제목 추가
plt.xlabel("X Label")
plt.ylabel("Y Label")
plt.show()
```
````python
# 그래프 상의 볼 범위를 지정할 수 있다.
plt.xlim(0,10) 
plt.ylim(0,10)
# 그래프의 크기 지정
plt.figure(figsize = (10, 20)) 
```

