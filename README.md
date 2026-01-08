# 📚 ShaderToy Fresnel Effect

## Project Overview

이 프로젝트는 **Schlick Fresnel Approximation**을 사용해 Specular 성분에 Fresnel 효과를 적용한 shader이다.

Fresnel 효과는 **view direction**과 **surface normal** 사이의 각도에 따라 reflection(반사) 비율이 변화하는 현상을 모델링한다. 특히 물체의 가장자리에서 반사가 강해지는 특성이 있어, 실시간 렌더링에서 재질의 특성(금속/유리/플라스틱)을 표현하는 데 사용된다.

본 구현에서는 Schlick 근사를 이용해 Fresnel 계수 F를 계산하고, 이를 specular 색상에 곱하여 시점 각도에 따른 반사 변화가 나타나도록 구성하였다.

---

## 📌 Key Concepts & Implementation

### **1) Schlick Fresnel Approximation**
   
  Schlick 근사는 Fresnel 방정식을 간단한 형태로 근사하여 실시간 렌더링에 적합하게 만든 방식이다.
  
  기본 형태는 다음과 같다.
  - `F = F0 + (1 - F0) (1 - N · V)^5`

  여기서:
  -  N · V : 표면 법선 N과 시점 방향 V의 내적
  -  F0 (fresnelR0) : **정면(0°)**에서의 반사율(재질 고유값)
  -  F : 각도에 따라 변하는 Fresnel 반사 계수
    
  `N · V` 값이 작아질수록(= 가장자리로 갈수록) `(1 − N · V)`가 커지고, 결과적으로 F → 1에 가까워져 반사 성분이 크게 증가한다.

---

### **2) Specular에 Fresnel 적용** 

  계산한 Fresnel 계수 F를 specular 성분에 곱해, 시점 각도에 따라 반사 강도가 달라지도록 한다.
  - `specular *= F`

  이를 통해:
  - **정면(0°)**에서는 F ≈ F0로 수렴하여 비교적 안정적인 specular 반사가 나타난다.
  - **가장자리(90°)**에서는 F → 1에 가까워져 specular 하이라이트가 강하게 강조된다.

---

### 🧩Code Snippet
<details>
  <summary><b></b></summary>

  <img width="720" alt="carbon (11)" src="https://github.com/user-attachments/assets/48676150-f4cd-4b91-9895-324de02cc692" />
</details>




## 📌 Sample Outputs

<img width="720" alt="스크린샷 2026-01-06 210336" src="https://github.com/user-attachments/assets/953d244b-ef9e-4dfc-9f3e-9a54e0ceef2d" />

---

## 📌 Future Work


---


## Development Environment

- Language: C++
- Graphics API: DirectX11
- Development Environment: Visual Studio 2022
- Build Configuration: x64, Debug / Release

### Hardware
- CPU: Intel CPU (Desktop)
- GPU: NVIDIA RTX 3060
- RAM: 16GB

### Platform
- OS: Windows 10 / 11
  
---

## References

- HongLab
  *Introduction to Computer Graphics with DirectX 11 – Part 2: Realtime Pipeline*
