# Allow-me-to-introduce-myself
이름, 나이, MBTI, 좋아하는 음식, 좋아하는 색상 등을 HTML 폼으로 입력 받고, Thymeleaf를 사용해 결과를 보기 좋게 출력해보는 프로젝트입니다.


1. HTML 입력 폼 구성
2. <img width="503" height="575" alt="스크린샷 2025-09-08 오후 7 25 38" src="https://github.com/user-attachments/assets/4ecab233-97e3-45cd-ad8d-7a5d1fbadbac" />

2.서버에서 입력값 처리 및 모델 전달

package kr.sparta.practical2_starter;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.PostMapping;

@Controller
public class IntroController {

    @Autowired
    private MbtiEmojiService mbtiEmojiService;

    // 1️⃣ 폼 화면
    @GetMapping("/")
    public String showForm(Model model) {
        model.addAttribute("person", new Person()); // Person 객체와 폼 연결
        return "introForm"; // templates/introForm.html
    }

    // 2️⃣ 폼 제출 후 결과 처리
    @PostMapping("/result")
    public String showResult(@ModelAttribute Person person, Model model) {
        // MBTI에 맞는 이모지 가져오기
        String mbtiEmoji = mbtiEmojiService.getEmoji(person.getMbti());

        // 모델에 폼 데이터와 이모지 담기
        model.addAttribute("person", person);
        model.addAttribute("mbtiEmoji", mbtiEmoji);

        return "introResult"; // templates/introResult.html
    }
}


3. 한 줄 자기소개 출력


    String intro = String.format(
                "안녕하세요! 저는 %d살이고 %s이며 %s를 좋아하고 %s을 좋아해요!",
                person.getAge(),
                person.getMbti(),
                person.getFavoriteFood(),
                person.getFavoriteColor()
        );


5. MBTI에 따라 이모지 출력하기


public static final Map<String, String> MBTI_EMOJI_MAP = Map.ofEntries(
    Map.entry("ISTJ", "📘"), // 신중한 관리자 – 책
    Map.entry("ISFJ", "🛡️"), // 헌신적인 수호자 – 방패
    Map.entry("INFJ", "🔮"), // 통찰력 있는 조언자 – 수정구슬
    Map.entry("INTJ", "♟️"), // 전략적인 사색가 – 체스말

    Map.entry("ISTP", "🛠️"), // 논리적인 장인 – 공구
    Map.entry("ISFP", "🎨"), // 예술적인 예민가 – 팔레트
    Map.entry("INFP", "🌸"), // 감성적인 중재자 – 벚꽃
    Map.entry("INTP", "💡"), // 논리적인 사색가 – 전구

    Map.entry("ESTP", "🏍️"), // 모험적인 활동가 – 오토바이
    Map.entry("ESFP", "🎉"), // 자유로운 연예인 – 폭죽
    Map.entry("ENFP", "🔥"), // 열정적인 외교관 – 불꽃
    Map.entry("ENTP", "⚡"), // 재기발랄한 발명가 – 번개

    Map.entry("ESTJ", "📋"), // 현실적인 관리자 – 체크리스트
    Map.entry("ESFJ", "🤝"), // 친화력 좋은 사회자 – 악수
    Map.entry("ENFJ", "🌟"), // 정의로운 주도자 – 별
    Map.entry("ENTJ", "👑")  // 당당한 리더 – 왕관

);

5.시연영상

![화면-기록-2025-09-08-오후-7 27 42](https://github.com/user-attachments/assets/803ee205-698a-445c-878c-42fd2e006bfb)


