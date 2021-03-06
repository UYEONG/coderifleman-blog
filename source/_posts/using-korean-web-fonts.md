---
title: 한글 웹 폰트 경량화해 사용하기
description: 폰트의 서브셋 개념을 소개하고 한글 웹 폰트 Note Sans CJK를 이용해 폰트를 경량화하는 이유와 그 방법을 소개합니다.
date : 2015-04-04
category:
    - Fonts
tags:
    - Web Fonts
    - Fonts
    - Noto Sans CJK
---

## 웹 폰트란? 

웹 폰트란 간단히 말해서 폰트파일(eot, woff 등)을 브라우저가 서버로부터 내려받아 사용하는 폰트를 말합니다. 이용자 컴퓨터에 설치돼 있지 않아도 폰트가 동작하기 때문에 조금 더 미려한 디자인을 가능하게 합니다.

{% figure web-fonts.01.png 'Google Fonts' '그림 1.Google Fonts' 400px %}

[Google Fonts](https://www.google.com/fonts)의 서비스를 이용하면 사용할수 있습니다만 조금 아쉬운 점이 있습니다. 바로 구글의 폰트 서버를 이용해야 한다는 점인데요. 간단하고 편한 방법이긴 하지만 구글 서버의 응답이 늦거나 어떤 장애가 발생했을 때 그로 인한 이슈가 뒤따른다는점이죠. 그래서 직접 웹 폰트를 내려받아 사용하고자 합니다.

{% alert info '예제 폰트' %}
여기서는 예제로 [Noto Sans CJK](https://developers-kr.googleblog.com/2014/07/cjkfont.html)를 사용합니다. Noto Sans CJK는 구글과 어도비가 합작한 중국어, 일본어, 한국어를 모두 완벽히 지원하는 웹 폰트입니다.
{% endalert %}

## Noto Sans CJK 다운로드

Noto Sans CJK는 [공식 홈페이지](https://www.google.com/get/noto/#/)에서 내려받을 수 있습니다. CJK는 중국(China), 일본(Japan), 한국(Korea)의 준말입니다. NotoSans는 거의 모든 언어를 지원하지만, 서비스 특성상 모든 언어를 지원할 필요는 없으므로 CJK KR 버전을 내려받습니다.

{% figure web-fonts.02.png 'NotoSans CJK KR 파일 리스트' '그림 2.NotoSans CJK KR 파일 리스트' 400px %}

압축을 풀고 용량을 확인하는 순간, 엄청난 크기에 절망합니다. 웹에서는 단 1MB도 큰 단위이기 때문에 웹 폰트를 사용할 엄두가 나지 않습니다.

## Subset(and Subsetting)

{% figure web-fonts.03.png 'Google의 Subset 개념도' '그림 3.Google의 Subset 개념도' 400px %}

아직 포기하기엔 이릅니다. 웹 폰트에는 서브셋이라는 개념이 있습니다. 서브셋은 말 그대로 특정 폰트의 하위 집합을 뜻합니다. 따라서 필요한 하위 집합만을 추린다면 파일의 용량은 처음보다 아주 작아질 것입니다.

{% alert info 'Google의 서브셋 기능' %}
Google Font 역시 [서브셋 기능](https://developers.google.com/fonts/docs/getting_started#specifying_script_subsets)을 제공하고 있습니다.
{% endalert %}

{% figure web-fonts.04.png 'NotoSans Subset 다운로드' '그림 4.NotoSans Subset 다운로드' 400px %}

[CJK 다운로드 페이지](https://www.google.com/get/noto/)에서 this folder 링크를 클릭합니다. 그리고 `NotoSansKR-*.otf` 한국어 서브셋 파일을 내려받고 확인합니다.

{% figure web-fonts.05.png 'NotoSans KR 파일 리스트' '그림 5.NotoSans KR 파일 리스트' 400px %}

이전 파일(약 16MB)과 비교하여 확실히 파일의 용량이 줄었습니다. 하지만 여전히 부담되는 용량입니다. 더 용량을 줄일 수 없을까요?

### 직접 Subset 지정하기

완성형일 경우 [엄청난 양의 한글](https://jrgraphix.net/r/Unicode/AC00-D7AF)이 필요하지만, 사실 모든 문자셋을 사용하진 않습니다. [KS X 1001 표준](https://ko.wikipedia.org/wiki/KS_X_1001)에는 자주 쓰이는 한글 2,350자를 정의하고 있습니다. 이 한글만 추려낸다면 용량을 많이 줄일 수 있을 것 같습니다.

{% figure web-fonts.06.png '서브셋 폰트 메이커와 WOFF컨버터' '그림 6.서브셋 폰트 메이커와 WOFF컨버터' 400px %}

이 문제와 관련된 유용한 애플리케이션을 찾았습니다. [서브셋 폰트 메이커](https://opentype.jp/subsetfontmk.htm)와 [WOFF 컨버터](https://opentype.jp/woffconv.htm)가 바로 그것입니다. 이 두 애플리케이션을 설치합니다.

{% figure web-fonts.07.png '서브셋 폰트 메이커 파입 입력 폼' '그림 7.서브셋 폰트 메이커 파입 입력 폼' 400px %}

그리고 서브셋 폰트 메이커에 NotoSans 폰트와 새로운 파일의 경로를 설정합니다.

{% figure web-fonts.08.png '서브셋 폰트 메이커 폰트 지정 폼' '그림 8.서브셋 폰트 메이커 폰트 지정 폼' 400px %}

그리고 폰트에서 남기고자 하는 한글(및 영어, 숫자, 특수문자)를 입력하고, WOFF 컨버터 실행에 체크합니다.

{% alert info '폰트 지원 여부' %}
[EOT](https://caniuse.com/#feat=eot)는 IE에서만 지원하는 문자 포멧입니다. [WOFF](https://caniuse.com/#feat=woff)또는 [OTF](https://caniuse.com/#feat=otf)는 모든 브라우저에서 지원합니다.
{% endalert %}

생성 시작 버튼을 클릭하면 폰트 파일이 생성된 후 WOFF 컨버터가 실행됩니다. 자동으로 경로가 입력되므로 별다른 설정 없이 변환시작 버튼을 선택해 변환합니다.

{% figure web-fonts.09.png '컨버터된 NotoSans KR 파일 리스트' '그림 9.컨버터된 NotoSans KR 파일 리스트' 400px %}

생성된 파일을 확인하면 4.7MB에서 200KB ~ 400KB 사이로 용량이 작아진걸 확인할 수 있습니다.

{% figure web-fonts.10.png '컨버터된 NotoSan KR 파일의 전체 용량' '그림 10.컨버터된 NotoSan KR 파일의 전체 용량' 320px %}

파일의 전체 용량도 이전 폰트 파일 1개의 용량 만큼 작아졌습니다. 브라우저는 자신이 지원하는 폰트 파일만 요청할 것이므로 폰트의 모든 굵기를 사용한다면 최대 약 1.6MB 정도 요구될 것 같네요. 보통 3~4가지의 굵기를 추려서 사용하므로 이 정도면 웹에서 사용해도 큰 부담이 없을 것 같습니다.

### 사용해보기

변환한 파일이 제대로 동작하는지 한번 사용해 보겠습니다.

{% codeblock lang:css %}
@font-face {
    font-family: 'Noto Sans';
    font-style: normal;
    font-weight: 100;
    src: local('Noto Sans Thin'), local('Noto Sans Thin'), local('Noto Sans Thin');
    src: url(NotoSansKR-Thin-subset.eot);
    src: url(NotoSansKR-Thin-subset.eot?#iefix) format('embedded-opentype'),
    url(NotoSansKR-Thin-subset.woff) format('woff'),
    url(NotoSansKR-Thin-subset.otf) format('truetype');
}

@font-face {
    font-family: 'Noto Sans';
    font-style: normal;
    font-weight: 300;
    src: local('Noto Sans Light'), local('Noto Sans Light'), local('Noto Sans Light');
    src: url(NotoSansKR-Light-subset.eot);
    src: url(NotoSansKR-Light-subset.eot?#iefix) format('embedded-opentype'),
    url(NotoSansKR-Light-subset.woff) format('woff'),
    url(NotoSansKR-Light-subset.otf) format('truetype');
}
... 이하 생략 ...
{% endcodeblock %}

먼저 css 파일에서 웹 폰트를 지정합니다.

{% codeblock lang:html %}
<style>
  span {font-family: 'Noto Sans';font-size: 20px}
</style>
<span style="font-weight: 100">모든 인간은 태어날 때부터 자유로우며 그 존엄과 권리에 있어 동등하다. 12345567890, ABCDEFG<br />
<span style="font-weight: 300">모든 인간은 태어날 때부터 자유로우며 그 존엄과 권리에 있어 동등하다., 12345567890, ABCDEFG<br />
<span style="font-weight: 350">모든 인간은 태어날 때부터 자유로우며 그 존엄과 권리에 있어 동등하다., 12345567890, ABCDEFG<br />
<span style="font-weight: 400">모든 인간은 태어날 때부터 자유로우며 그 존엄과 권리에 있어 동등하다., 12345567890, ABCDEFG<br />
<span style="font-weight: 500">모든 인간은 태어날 때부터 자유로우며 그 존엄과 권리에 있어 동등하다., 12345567890, ABCDEFG<br />
<span style="font-weight: 700">모든 인간은 태어날 때부터 자유로우며 그 존엄과 권리에 있어 동등하다., 12345567890, ABCDEFG<br />
<span style="font-weight: 900">모든 인간은 태어날 때부터 자유로우며 그 존엄과 권리에 있어 동등하다., 12345567890, ABCDEFG
{% endcodeblock %}

그리고 이 폰트를 사용해 HTML에 적용합니다.

{% figure web-fonts.11.png 'NotoSans 폰트 사용 결과' '그림 11.NotoSans 폰트 사용 결과' 400px %}

## 끝으로

매번 웹 폰트를 사용할 때마다 위에서 소개한 서브셋 폰트 메이커와 WOFF 컨버터를 이용해 필요한 문자만 추출하는 작업을 반복할 순 없을 것 입니다. 서비스의 특성에 따라 필요한 문자셋도 다를 것이며 간단해 보이지만 의외로 반복적이고 따분한 작업입니다. 이를 간단하게 자동화하거나 문자셋을 몇 가지 패턴으로 나눠 중앙 서버에서 제공해주는 방법을 고려해보는 게 좋을 것 같습니다. 이를 위해선 현재 애플리케이션의 원리를 분석하여 환경에 맞는 애플리케이션을 새롭게 개발해야 할 수도 있습니다.(원리는 단순히 유니코드를 비교하여 필터링하는 것으로 보입니다.)

이것으로 필요한 문자만 나두고 나머지를 전부 제거하는 방식으로 웹 폰트 용량을 경량화 하는 방법에 대해 알아봤습니다. 만약 폰트에 없는 문자를 작성하게 되면 폰트가 깨질 것입니다. 따라서 댓글과 같이 어느 나라 유저가 어떤 문자를 작성할 지 모르는 기능에는 이 방식으로 웹 폰트를 지원하기는 힘들 것입니다. 하지만 사이트의 타이틀, 설명구, 메뉴, 아티클 등에는 이러한 방식으로 경량화하여 웹 폰트를 충분히 지원할 수 있을 것 같습니다.

잘못된 폰트 파일이 웹상에 퍼질까봐 노파심에 파일을 공개적으로 공유하지 않았지만, 생각지 못하게 경량화한 폰트 파일을 달라는 요청이 많아서 [깃허브 저장소](https://github.com/UYEONG/NotoSans-subset)에 올려두었으니 참고하시길 바랍니다.

## 버그

인터넷 익스플로러(이하 IE)에는 다양한 웹 폰트 버그가 있기 때문에 서비스 정책상 구 버전 IE를 지원해야 한다면 웹 폰트를 사용하기 싫어질 수 있습니다. 제가 겪는 문제를 이 곳에 조금씩 정리해나갈 생각이지만 잠재적인 버그가 워낙 많기 때문에 이 외에도 다양한 문제를 마주할 수 있습니다.

### IE8에서 가중치(weight)가 동작하지 않는 문제

첫 번째로 `font-face`를 이용해 다양한 가중치를 선언하면 IE8에서 특정 가중치가 동작하지 않는 문제가 있습니다.

{% codeblock lang:css %}
@font-face {
    font-family: 'Noto Sans';
    font-style: normal;
    font-weight: 300;
    src: local('Noto Sans Light'), local('Noto Sans Light'), local('Noto Sans Light');
    src: url(./NotoSansKR-Light.eot);
    ... 생략 ...
}

@font-face {
    font-family: 'Noto Sans';
    font-style: normal;
    font-weight: 400;
    src: local('Noto Sans Regular'), local('Noto Sans Regular'), local('Noto Sans Regular');
    src: url(./NotoSansKR-Regular.eot);
    ... 생략 ...;
}

.f {font-family: 'Noto Sans'}
.fw300 {font-weight: 300}
.fw400 {font-weight: 400}
.fw500 {font-weight: 500}
.fw700 {font-weight: 700}
{% endcodeblock %}

보통 위와 같은 방식으로 `font-face`를 선언하고 가중치를 이용해 다양한 굵기의 폰트를 사용합니다.

{% figure web-fonts.12.png 'Firefox와 IE8의 폰트 출력 결과' '그림 12.Firefox와 IE8의 폰트 출력 결과' 400px %}

위 그림을 보면 파이어폭스에서는 의도한대로 출력되지만 IE8에서는 `font-weight: 300`, `400`, `500`으로 선언한 폰트가 동일한 굵기로 출력되는 것을 볼 수 있습니다. 이 문제는 하나의 폰트 명으로 묶지 않고 각각 폰트 명을 지정하는 방법으로 회피할 수 있습니다.

{% codeblock lang:css %}
.fw300 {font-family: 'Noto Sans Light'}
.fw400 {font-family: 'Noto Sans Regular'}
.fw500 {font-family: 'Noto Sans Medium'}
.fw700 {font-family: 'Noto Sans Bold'}
{% endcodeblock %}

위 코드를 IE8로 실행해보면 다음과 같이 출력됩니다.

{% figure web-fonts.13.png 'IE8의 폰트 출력 결과' '그림 13.IE8의 폰트 출력 결과' 400px %}

IE8의 버그를 회피하고자 폰트 명을 여러개로 분할했습니다. 개발이나 유지보수 차원에서 그다지 좋은 방식은 아닌것 같아 아쉽습니다. 이와 관련된 버그는 [Using multiple weights and styles](https://helpx.adobe.com/fonts/using/css-selectors.html)에 잘 정리돼 있습니다.

### IE8에서 특수 문자가 비정상적으로 출력되는 문제

위에서 서브셋을 직접 지정하는데 `NotoSansKR-*.otf` 파일을 사용했습니다. 추출한 폰트 파일을 IE8에서 사용하면 특수문자가 비정상적으로 출력되는 문제가 있습니다.

{% figure web-fonts.14.png 'Firefox와 IE8의 특수문자 출력 결과' '그림 14.Firefox와 IE8의 특수문자 출력 결과' 400px %}

키보드로 입력 가능한 특수문자인 -(dash), |(vertical bar) 등이 잘못 렌더링 되는 문제입니다. 아직 정확한 원인은 파악하지 못했지만 폰트 파일과 직접적인 영향이 있는것으로 추측되어 파일을 `NotoSansKR-*.otf`이 아닌 `NotoSansCJKkr-*.otf`로 변경하여 다시 추출했습니다.

NotoSansCJKkr은 NotoSansKR에 비해 용량이 3배 이상 많으므로 다양한 문자를 포함하고 있으니 원하는 문자를 추출할 수 있을 것 같았습니다. 추출 후의 파일 용량은 약 2KB 정도 차이 납니다.

{% figure web-fonts.15.png 'IE8의 특수문자 출력 결과' '그림 15.IE8의 특수문자 출력 결과' 400px %}

새로 추출한 폰트 파일로 변경하고 IE8에서 실행하면 정상적으로 출력됩니다.
