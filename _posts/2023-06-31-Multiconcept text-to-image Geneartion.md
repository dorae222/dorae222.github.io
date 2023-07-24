---
layout: post
title: Multi-concept text to image Generation
subtitle: Multi-concept text to image Generation
categories: 프로젝트
tags: [StableDiffusion, MultiConcept]
---
<br>

## INTOON

---

![image](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/05475437-be29-4fc7-a6c6-41467cd1837e)


기간: 2023.04 ~ 2023.06

### 프로젝트 요약

---

- 이미지 생성시 컨셉을 유지/적용하는 방법(Textual Inversion, Hyper Network, Dreambooth, LoRA 등)을 동시에 여러 컨셉으로 적용하면, 원치 않게 혼합되는 경우들이 발생

- 컨셉의 종류와 범위에 따라 서로에게 간섭을 최소화하여 원하는 대로 이미지를 생성하는 기술을 연구개발


<details>
<summary>프로젝트 세부 내용</summary>


<details>
<summary>I. Proposal</summary>

- 연구 내용
    - 이미지 생성시 컨셉을 유지/적용하는 방법(Textual Inversion, Hyper Network, Dreambooth, LoRA 등)을 동시에 여러 컨셉으로 적용하면, 원치 않게 혼합되는 경우들이 발생
    - 컨셉의 종류와 범위에 따라 서로에게 간섭을 최소화하여 원하는 대로 이미지를 생성하는 기술을 연구개발
- 연구 목적
    - Generative AI는 생성 품질면에서 많은 성장을 이루고 있으며, 서비스로도 활용되고 있으나 2가지 이상의 컨셉을 적용하는 것은 도전적인 영역
    - 단일 컨셉으로 생성된 이미지와 비교해서 보다 풍부하고 다양한 정보를 담을 수 있어 더욱 현실감 있고 창의적인 이미지를 생성할 수 있음
    - Multi-concept diffusion 기술을 발전시킴으로써 다양한 분야에서의 응용 가능성을 높이고, 이미지 생성 기술의 응용 범위를 확장할 수 있는 기반 생성
- 활용 계획
    - 멀티 컨셉을 활용한 이미지 생성 서비스 적용
- 프로젝트 소개
    - 매번 생성할 때마다 대상이 너무 크게 변합니다. 예를들어서, 강아지를 생성한다고 하면 매 생성 때마다 다른 강아지가 생성될 것입니다. 따라서 사용자는 자신의 컨셉(얼굴, 애완동물, 장소, 옷 등)을 활용하여 이미지를 생성하고자 할 때가 있습니다. 소수의 샘플 이미지를 통해 새로운 컨셉을 빠르게 학습하고, 이를 반영하는 것은 이미지 생성서비스에 사용자가 큰 만족감을 느낄 수 있습니다.
    - 새로운 컨셉을 학습하고 적용하는 방법에는 Texutal Inversion, Hyper Network, Dreambooth, LoRA 등 다양한 방법들이 있습니다. 그런데, 적용하고자하는 새로운 컨셉이 2개 이상인 경우 mixing되어 나타나는 문제가 있습니다. 예를 들어 남녀 커플 2명을 학습하는 경우 두 얼굴의 개성이 섞여 나타나곤 합니다.
    - 이를 개선하기 위한 다양한 시도들이 제시되고 있으며, 이러한 것들을 기술적으로 비교하고 개선을 시도하는 것이 이번 프로젝트의 목표입니다.
    - 예시
        
        ![image](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/d8fbc748-3720-48a4-b1ca-0e1608a25ff8)
        
</details>

<details>
<summary>II. Related Work (e.g., existing studies)</summary>

- Stable diffusion이란?
    
    ![Untitled 1](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/be94b23b-7805-4dee-877d-222effe0f396)
    
    ![Untitled 2](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/f0bd170f-8776-46c6-9bed-dd0e344f30f5)
    
    ![Untitled 3](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/8a768bbd-3089-4fcd-b95e-16b35e170e8c)
    
    ![Untitled 4](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/57a5cb94-477b-47b1-9c68-5a174d93b1d8)
    
    ![Untitled 5](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/c00ed0c9-9bae-436b-bf9b-20b51395b629)
    
- Fine Tuning
    
    ![Untitled 6](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/8160ff60-1a43-4c70-b2b1-cb047e9d39d1)
</details>    

<details>
<summary>III. 문제정의</summary>

- 연구 목적과 동일
    
    
    ![Untitled 7](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/3b7d0b74-3a70-4310-b6ba-a9d06c58c528)
    
    ![Untitled 8](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/b1f4a5d0-d420-4308-8d61-d16f962e823a)
    
- 원인 분석
    
    ![Untitled 9](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/f062e96d-30d9-4219-be1c-6e537f56e895)
    
    ![Untitled 10](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/9e6a5d95-3963-43fc-8905-f780df71663d)
    
    ![Untitled 11](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/66014bde-b595-480b-b246-2b45fa4ac3f6)
    
</details> 

<details>
<summary>IV. 해결 방안</summary>

- Training
    
    ![Untitled 12](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/ed765594-d21c-49c2-b472-a1354b7c64c9)
    
- Inference
    
    ![Untitled 13](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/daf1380d-57db-42bd-b0b7-6f69d9d605d5)
    
</details> 

<details>
<summary>V. 예상 결과 및 기대효과</summary>

![Untitled 14](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/542b139a-8b15-452f-91a6-4af99f0c7a81)

</details>

<details>
<summary>VI. 연구과제 수행 계획</summary></details> 


- 연구 계획 일정
    
    ![Untitled 15](https://github.com/jeffreytse/jekyll-theme-yat/assets/105966480/2aa7e49b-eeb9-4343-9ed1-e3c968275171)

</details>

### 산출물

---

- [발표 PDF](https://drive.google.com/drive/folders/13J7aLt_1NRZUQAXyzAghcbSUUVyCH-J4?usp=sharing)<br>
- [참고 노션](https://www.notion.so/dorae222/Multi-concept-text-to-image-Generation-ef93cea3fec441909cd98e38c3475b63?pvs=4)