//node 는 실행단위 (병렬수행)
//stage 는 단계 (단계적수행)
//구성순서는 상관없음

//마이크로서비스 별 단계
node('mas-service-coffee-order', { 
  stage('stage-1', { 
    echo "hello coffee order 1 stage" 
  }) 
  stage('stage-2', { 
    echo "hello coffee order 2 stage" 
  }) 
  stage('stage-3', { 
    echo "hello coffee order 3 stage" 
  }) 
}) 

/*
stage('example2', { 
  node('', { 
    echo "" 
  }) 
})
*/
