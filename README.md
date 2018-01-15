게시판 만드는데 게시글 옆에 댓글갯수

reference
post:reference

rails g model comment post_id:integer content:text

rails goreign key

폼태그 이렇게도 만드는것이 가능
<form action='/posts/comment' method='post'>
<input name='content />
<input hidden='post_id' value = '<%=@post.id %>
<input type = 'submit' />
</form>



SELECT2


Post.all.eager_load(:comments)

Post.all.includes(:comments)
Post.all.preload(:comments)

컨트롤러 이렇게만듬
  def index
    @posts = Post.all.includes(:comments)
  end

그럼 includes로 바뀜


Post.includes(:tags).where(tags=> ({content: 'faker'})
이렇게 하면 태그가 페이커인것만 찾음
근데 관계설정 해줘야됨 post에다가 has_many :faker 해줘야 함
그리고 tag란모델을 임의적으로 만들어줘야 됨
근데 preload는 안됨이거


결과적으로 includes를 쓰는게 편함
Comment.includes(:post)



mark down



gfm


simple mde

여기가서
<link rel="stylesheet" href="https://cdn.jsdelivr.net/simplemde/latest/simplemde.min.css">
<script src="https://cdn.jsdelivr.net/simplemde/latest/simplemde.min.js"></script>

복붙

board\app\views\posts\_form.html.erb
여기로가서
<script>
var simplemde = new SimpleMDE();
</script>
이걸 form_for 안에다 넣기

자바스크립트버전
<script>
var simplemde = new SimpleMDE({ element: document.getElementById("MyID") });
</script>

Jquery 버전
<script>
var simplemde = new SimpleMDE({ element: $("#MyID")[0] });
</script>


근데 요즘 이런거 씀
we don't need Jquery


gem redcarpet


마크다운 파서
markdown = Redcarpet::Markdown.new(renderer, extensions = {})
markdown.render("This is *bongos*, indeed.")
포스트컨트롤러의 show에다가 복붙하기

근데 그대로하면 렌더러 에러뜸

  markdown = Redcarpet::Markdown.new(Redcarpet::Render::HTML, extensions = {})

두줄 지우고 이렇게 해야됨

그리고 쇼페이지가서 content 수정
  <%= @markdown.render(@post.content).html_safe %>
