# 강채린 포트폴리오
> 이메일 : rkdcofls0828@gmail.com
> 
> 깃허브 : https://github.com/kangchaelin
<br>

![image](https://github.com/kangchaelin/PORTFOLIO/assets/142488328/710e5aa0-6774-4cdf-9c8c-9b7620b0d8a9)


# 🍀 PicStory
> 🏅 최우수상 수상
> 
> AI 기술을 활용한 이미지 태깅 기반의 사진첩 서비스
>
>개발 기간: 2024.02.01 ~ 2024.02.28
>
>참여 인원: 팀프로젝트(5명)

<br>

![image](https://github.com/kangchaelin/PORTFOLIO/assets/142488328/486a4f91-cd0d-4e33-9631-5f7be2208d55)

# 🍀 YOU & I
>클라우드 기반 공통 취미를 공유하는 지역 소모임 관리 플랫폼
>
>개발 기간: 2023.11.22 ~ 2023.12.08
>
>참여 인원: 팀프로젝트(5명)

<details>
<summary>상세 보기</summary>

## 👀 서비스 소개
저희 서비스는 지역과 취미를 기반으로 그룹을 생성하고, 사용자들에게 다양한 경험을 쌓
을 수 있는 소통의 창구를 제공하는 것을 목표로 합니다. 사용자들은 자신의 지역 또는 취
미에 관련된 그룹을 찾아 가입하여 새로운 사람들과의 만남 및 소통의 기회를 가질 수 있
습니다.

<br>

## 📅 프로젝트 기간 및 참여인원
> 2023년 11월 22일 ~ 2023년 12월 8일
> 
> 참여 인원: 팀프로젝트(5명)
<br>

## ⚙ 시스템 아키텍처
![image](https://github.com/kangchaelin/PORTFOLIO/assets/142488328/7a2ed62f-5431-4c09-bee8-ae7a4b2f1fb0)
<br>

## 📌 서비스 흐름도
![image](https://github.com/kangchaelin/PORTFOLIO/assets/142488328/c230a70b-0616-4359-8638-8f22b8da580a)

<br>

## 📌 ER다이어그램
![image](https://github.com/kangchaelin/PORTFOLIO/assets/142488328/01e0101a-8a72-430d-b4e7-22ecd1ac5ff0)

<br>

## ⭐ 나의 역할: Back-End & Front-End
- HTML과 CSS를 활용하여 마이페이지 및 메인페이지의 레이아웃과 디자인 작업
- JavaScript와 jQuery 라이브러리를 활용해 회원정보 수정 및 회원탈퇴 기능 구현

<details>
   <summary>Front</summary>
      <br/>
<div align="center">
<div><메인페이지></div>
<img src="https://github.com/kangchaelin/kangchaelin/assets/142488328/f2917c27-0407-4a10-a360-9db64ac7ee29" width="400" />
    <br>
    <br>
<div><마이페이지></div>
<img src="https://github.com/kangchaelin/kangchaelin/assets/142488328/23454ea0-dce3-4325-82f8-a0cd4c920201" width="400" />
</div>
</details>

<details><summary>Back</summary>
<br>
<h5>📍 회원 정보 수정</h5>
<p>1. 마이페이지 화면에서 수정사항을 변경합니다.</p>
<p>2. 적용 버튼을 클릭하면 입력란이 읽기전용으로 변경되며, 변경 사항이 DB에 업데이트 됩니다.</p>

<div><h6>mypg.html</h6></div>
<div markdown="1">

     // 적용 버튼을 클릭하면 이벤트 발생
     $("#mybtn").on("click", () => {
       var inputValues = [];
       // input태그(닉네임, 연락처, 활동지역)에 정보를 입력받고, 입력받은 데이터를 inputValues 리스트에 추가
       $(".ip").each(function() {
       var value = $(this).val();
       inputValues.push(value);
     });
     var mypCtValues = [];
   
     // select태그에 정보를 입력받고, 입력받은 데이터를 mypCtValues 리스트에 추가
     $(".mypCt").each(function() {
       var value = $(this).val();
       mypCtValues.push(value);
     });
   
     var sendObj = { nick: inputValues[0], phone: inputValues[1], region: inputValues[2], ct1: mypCtValues[0]};
   
     $.ajax({
        // UpdateMyPage.do페이지에 요청
        url: "UpdateMyPage.do",
         // UpdateMyPage.do페이지에 데이터 보내기
        data: sendObj,
        dataType: "json",
        success: function() {
       },
       error: function(e) {
       }
       })
    })

</div>

<div><h6>UpdateMyPageService.java</h6></div>
<div markdown="1">
      
      public class UpdateMyPageService implements Command {
      @Override
      public String execute(HttpServletRequest request, HttpServletResponse response)
         throws ServletException, IOException {
   
         request.setCharacterEncoding("utf-8");
         response.setContentType("text/html;charset=utf-8");
         
         HttpSession session = request.getSession(); 
         String user_id = (String) session.getAttribute("id");
         String nick =request.getParameter("nick");
         String phone =request.getParameter("phone");
         String region =request.getParameter("region");
         String ct1 =request.getParameter("ct1");
     
         User_DTO u_dt = new User_DTO();
         u_dt.setId(user_id);
         u_dt.setNick(nick);
         u_dt.setPhone(콜);
         u_dt.setRegion(region);
         u_dt.setHobby(ct1);
         
         User_DAO dao = new User_DAO();
         int row = dao.update(u_dt);
         
         if(row > 0 ) {
            return "redirect:/Gomypg.do";
         }
         else {
            return "redirect:/Gomypg.do";
         }
      }
      }
    
</div>

<div><h6>User_DAO : update()</h6></div>
<div markdown="1">
     
     public int update(User_DTO dto) {
        SqlSession sqlSession = factory.openSession(true);
        int row = sqlSession.update("update", dto);
        sqlSession.close();
        return row;
     }

</div>

<div><h6>Mapper.xml : id="update"</h6></div>
<div markdown="1">
   
     <update id="update" parameterType="com.YOU_I.model.User_DTO">
        UPDATE tbl_user
        SET
        nick=#{nick}, phone=#{phone}, region=#{region}, hobby=#{hobby}
        WHERE id = #{id}
     </update>

</div>



<h5>📍 회원 탈퇴</h5>
<p>1. 마이페이지 화면에서 회원탈퇴 버튼을 클릭합니다.</p>
<p>2. 아이디와 비밀번호를 입력하고 확인을 클릭합니다.</p>
<p>3. 정보가 일치하면 회원 탈퇴가 완료되며, 메인페이지로 이동합니다.</p>

<div><h6>mypg.html</h6></div>
<div markdown="1">

        // 탈퇴 버튼을 클릭하면 이벤트 발생
        $("#popupsub").on("click", function() {
        
          var sendObj = { id: $("#userId").val(), pw: $("#userPw").val() };
          $.ajax({
    
             url: "unregister.do",
             data: sendObj,
             dataType: "json",
             success: function() {
    
                alert("회원탈퇴에 성공하셨습니다. 이용해주셔서 감사합니다.");
                window.location.href =    "http://localhost:8081/YOU_I/Gomainpg.do";
             },
             error: function(e) {
                alert("아이디와 비밀번호가 일치하지않습니다.");
             }
             })
          })
       }

</div>

<div><h6>unregisterService.java</h6></div>
<div markdown="1">
      
       public class unregisterService implements Command {
       @Override
       public String execute(HttpServletRequest request, HttpServletResponse response)
             throws ServletException, IOException {
             response.setContentType("text/html;charset=utf-8");
          PrintWriter out = response.getWriter();
    
          String u_id = request.getParameter("id");
          String u_pw = request.getParameter("pw");
    
          User_DTO u_DTO = new User_DTO();
          u_DTO.setId(u_id);
          u_DTO.setPw(u_pw);
    
          User_DAO dao = new User_DAO();
          int res = dao.unregister(u_DTO);
          
          if(res>0) {
             out.print("{\"name\":\""+res+"\"}");   
          }
          return null;
       }
    
       }   
    
</div>

<div><h6>User_DAO : unregister()</h6></div>
<div markdown="1">
       
          public int unregister(User_DTO dto) {
          
          SqlSession sqlSession = factory.openSession(true);
          int res = sqlSession.delete("unregister", dto);
          sqlSession.close();
          return res;
          
       }

</div>

<div><h6>Mapper.xml : id="unregister"</h6></div>
<div markdown="1">
   
       <delete id="unregister" parameterType="com.YOU_I.model.User_DTO">
          DELETE FROM TBL_USER
          WHERE
          id = #{id} AND pw = #{pw}
       </delete>

</div>
</details>

 

</br>

## ⭐ 트러블슈팅
### ✅ 회원 탈퇴 시 모든 테이블에서 회원 정보가 삭제되지 않는 문제 발생
    
- **원인**: 초기에 테이블 설계 시 외래 키 제약 조건에 Cascade 옵션이 올바르게 설정되지 않아 발생

- **해결 방법**: 데이터베이스에서 각 테이블의 외래 키 제약 조건을 확인한 후 `ALTER TABLE` 문을 사용하여 올바른 설정으로 변경

<br>




## ⛏ My skils
<div>
            <img src="https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=java&logoColor=white"/>
            <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=HTML5&logoColor=white"/>
            <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=CSS3&logoColor=white"/>
            <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=JavaScript&logoColor=white"/>
            <img src="https://img.shields.io/badge/Eclipse-2C2255?style=for-the-badge&logo=Eclipse&logoColor=white"/>
            <img src="https://img.shields.io/badge/Oracle 11g-F80000?style=for-the-badge&logo=Oracle&logoColor=white"/>
            <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=GitHub&logoColor=white"/>
</div>

</details>

</details>

