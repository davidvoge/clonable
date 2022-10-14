//Load GSAP//
loadScriptFile("https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.1/gsap.min.js");
}
loadScriptFile("https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.1/Flip.min.js");
}

function loadScriptFile(src) {
  const $script = $("<script>");
  $script.attr("type", "text/javascript");
  $script.attr("src", src);
  $script.appendTo("head");
}

var element = document.getElementById("multistep_element");
element.classList.add("ready");

// IMAGE TRANSITION
var errorMessage = $(".error-message").text();
load();
$(".next-button").on("click", nextSlide);
$(".previous-button").on("click", prevSlide);
$(".send-button").on("click", function () {
  let formStep = $(this).closest(".multistep_slide-wrapper");
  let inputAvailable = $(formStep).find("input, select, textarea").length;
  $(formStep)
    .find("input, select, textarea")
    .each(function () {
      let isCompleted = $(this).val();
      if (isCompleted === "") {
        $(this)
          .closest(".multistep_input-wrapper")
          .append("<div class='error-message'>" + errorMessage + "</div>")
          .show();
      } else {
        $(".error-message").remove();
      }
    });
});

function nextSlide() {
  let formStep = $(this).closest(".multistep_slide-wrapper");
  let inputAvailable = $(formStep).find("input, select, textarea").length;
  let errorstate = 3;
  if (inputAvailable > 0) {
    $(formStep)
      .find("input, select, textarea")
      .each(function () {
        let isCompleted = $(this).val();
        if (isCompleted === "") {
          $(this)
            .closest(".multistep_input-wrapper")
            .append("<div class='error-message'>" + errorMessage + "</div>")
            .show();
        } else {
          $(".error-message").remove();
        }
      });
    errorstate = $(".error-message").length;
    if (errorstate === 0) {
      acceptchange();
    }
  } else {
    acceptchange();
  }

  function acceptchange() {
    let formIndex = $(formStep).index();
    let nextStepIndex = formIndex + 1;
    let nextStep = $(".multistep_slide-wrapper").eq(nextStepIndex);
    let state = Flip.getState(formStep);
    $(formStep).removeClass("visible");
    $(nextStep).addClass("visible");
    Flip.from(state, {
      targets: nextStep,
      duration: 0.5,
      absolute: true,
      ease: "power1.inOut"
    });
  }
}

function prevSlide() {
  let formStep = $(this).closest(".multistep_slide-wrapper");
  let formIndex = $(formStep).index();
  let prevStepIndex = formIndex - 1;
  let prevStep = $(".multistep_slide-wrapper").eq(prevStepIndex);
  let state = Flip.getState(formStep);
  $(formStep).removeClass("visible");
  $(prevStep).addClass("visible");
  Flip.from(state, {
    targets: prevStep,
    duration: 0.5,
    absolute: true,
    ease: "power1.inOut"
  });
}

function load() {
  $(".visible").removeClass("visible");
  $(".multistep_slide-wrapper").eq(0).addClass("visible");
  $(".placeholdercontent").each(function () {
    let placeholderContent = $(this).text();
    let encodedvalue = placeholderContent.toLowerCase().replace(" ", "-");
    $(this)
      .closest(".multistep_input-wrapper")
      .find("input")
      .attr("placeholder", placeholderContent)
      .attr("id", encodedvalue)
      .attr("name", encodedvalue)
      .attr("data-name", encodedvalue);
    $(this).remove();
  });
  $(".optionelement").each(function () {
    let optionText = $(this).text();
    let optionValue = optionText.toLowerCase();
    let select = $(this).siblings("select");
    $(select).append(new Option(optionText, optionValue));
    $(this).remove();
  });
  $(".error-message").remove();
}
