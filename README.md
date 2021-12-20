# Finalproject

우선 이 프로젝트를 시작하면서 우리가 수업시간에 배웠던 perceptron이랑 logistic regression 중 하나를 선택하여 실행하기로 생각했습니다.
왜냐하면 직접 배운 방법들로 접근하여야 그나마 배우지 않았던 방향보다는 더욱 정확도가 높아지지 않을까 하는 생각이였습니다.

그래서 먼저 순정 하이퍼파라미터로 perceptron, logistic regression을 시행해본 결과, logistic regression 쪽의 정확도가 더 높게 나왔었기 때문에,
logistic regression으로 프로젝트를 진행하며 하이퍼파라미터 튜닝을 시작하게 되었습니다.

traning dataset은 The Olivetti faces dataset을 사용하였습니다.

먼저 logistic regression의 순정 하이퍼파라미터의 경우, 그대로 알고리즘을 실행할 시에

STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.

Increase the number of iterations (max_iter) or scale the data as shown in:
    https://scikit-learn.org/stable/modules/preprocessing.html
Please also refer to the documentation for alternative solver options:
    https://scikit-learn.org/stable/modules/linear_model.html#logistic-regression
  n_iter_i = _check_optimize_result(
  
라는 오류 문구가 발생하였습니다. 찾아보니 이는 max_iter가 충분히 크지 않아서 나는 오류 메시지였고,
max_iter를 충분한 만큼의 값으로 올려주자, 오류 메시지도 발생하지 않았고, 정확도도 올라감을 확인할 수 있었습니다.

이후, 각 하이퍼파라미터 값들의 최적화를 위한 Randomized Search를 시행하였는데요.
이를 통하여 나온 각 하이퍼파라미터의 값들의 의의는 다음과 같았습니다.

penalty='l2', //이의 경우는 l2 > l1 > none 순으로 정확도의 차이를 보였으며, elasticnet의 경우는 계산의 속도가 너무 느려 해당 값은 포기하였습니다.

dual=False, //True와 False의 정확도 차이가 나타나지 않았습니다
    
tol=0.0001, //tol의 경우 올라갈 수록 정확도가 확연하게 떨어졌으며, 낮추는 방향은 어느 순간부터 정확도 값이 고정되었습니다.
    
C=1.0, //C값이 제가 Randomized Search로 구한 가장 의미있는 값이였는데, C=1000의 경우에서 정확도가 가장 높았으며, 이보다 높이거나 줄일경우 점점 정확도가 떨어졌습니다.
    
fit_intercept=True, //이는 True > False 로 정확도의 차이를 보였습니다.

intercept_scaling=1, //정확도에 영향을 끼치는 값을 찾지 못 했습니다.

class_weight=None, //정확도에 영향을 끼치는 값을 찾지 못 했습니다.

random_state=None, //정확도에 영향을 끼치는 값을 찾지 못 했습니다.

solver='lbfgs', //페널티의 종류에 영향을 끼치므로 정확도에 끼치는 영향은 없습니다.

max_iter=100, //위에서 보인대로 충분히 값을 높여줘야 모든 계산을 완료할 수 있고, 충분한 크기 이후로는 더욱 늘려도 영향을 끼치지 못했습니다.

multi_class='auto', //정확도에 영향을 끼치는 값을 찾지 못 했습니다.

verbose=0, //정확도에 영향을 끼치는 값이 아닙니다.

warm_start=False, //정확도에 영향을 끼치는 값을 찾지 못 했습니다.

n_jobs=None, //정확도에 영향을 끼치는 값을 찾지 못 했습니다.

l1_ratio=None, //elasticnet의 경우 사용하는 값이지만, 해당 페널티를 사용하지 않았으므로 의미없는 값입니다.

이러한 하이퍼파라미터 튜닝을 통해서 제가 가장 높게 구한 해당 traning dataset에 대한 정확도는 0.98이였습니다.
