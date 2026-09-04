VLM so good, but only 2D에 국한되어 있음. 3D volumetric data는 다루기 힘들다!

3D volumetric data를 처리하기 위해선 continuous 2D slice가 필요

이때 막대한 **anatomical redundancy**의 문제가 발생, 고정된 **pruning ratio**를 사용하기 때문에 서로 다른 slice에 존재하는 이질적인 **heterogeneous information densities**를 유연하게 처리 불가

여기서 heterogeneous information densities(이질적인 정보 밀도)란, 3D CT/MRI의 모든 slice가 똑같이 중요한 정보를 담고 있지 않다는 의미이다. 
예를 들어 어떤 slice에는 종양의 경계, 장기 구조, 병변처럼 중요한 정보가 많이 들어 있을 수 있지만, 다른 slice에는 거의 균일한 정상 조직이나 배경만 존재할 수 있다.

만약 중요한 token이 80개 10개인 slice A, B가 있다고 가정하면, 똑같이 80%씩 pruning하면 A는 중요한 정보도 제거될 수 있고, B는 중요하지 않은 내용을 많이 남기게 된다.

이때 고정된 pruning ratio를 사용하면 문제가 발생. 따라서 동적인 pruning ratio를 세팅

**“3D 의료영상에서는 slice마다 진단적으로 유용한 정보량이 다르므로, 모든 slice에 동일한 pruning 비율을 적용하는 것은 최적의 방법이 아니다”**

**“기존 pruning은 정적인 ratio를 사용하였지만, MedPruner는 동적인 ratio를 설정하여 유기적으로 최적화”**

**첫째, 3D 의료영상에서는 연속 slice가 매우 비슷한데도 기존 방식은 각 slice의 token을 그대로 이어 붙여서 slice 간 중복(inter-slice redundancy)이 커진다.**

**둘째, 기존 pruning 방법은 고정된 pruning ratio를 사용하기 때문에 slice마다 다른 정보 밀도와 모델마다 다른 attention 분포를 반영하지 못한다.**

MedPruner제안 > 3D의료영상 이해를 위해 특별히 설계된 training-free model -agnostic hierarchical token pruning framework

2가지 아이디어를 제시

IAF : 이 2D 사진 자체가 앞의 사진과 너무 비슷한가?
DINS : 이 사진 안에서도 어떤 영역의 token이 정말 중요한가?
