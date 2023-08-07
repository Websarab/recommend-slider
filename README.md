# recommend-slider


$( document ).ready(function() {
 setTimeout(function(){ 
$('.recommend').slick({
  dots: true,
  infinite: false,
  speed: 300,
  slidesToShow: 4,
  slidesToScroll: 4,
  responsive: [
    {
      breakpoint: 1024,
      settings: {
        slidesToShow: 3,
        slidesToScroll: 3,
        infinite: true,
        dots: true
      }
    },
    {
      breakpoint: 600,
      settings: {
        slidesToShow: 2,
        slidesToScroll: 2
      }
    },
    {
      breakpoint: 480,
      settings: {
        slidesToShow: 1,
        slidesToScroll: 1
      }
    }
    // You can unslick at a given breakpoint now by adding:
    // settings: "unslick"
    // instead of a settings object
  ]
});
     }, 2000);
  });	








  
<div class="acnav">
  <h2 class="category_title_Sel"> {{ section.settings.cat }} </h2>
<ul class="acnav__list acnav__list--level1">
{% for link in section.settings.menu.links %}
{% if link.links == blank %}
<li class="has-children">
  <a class="toggles new-sub"  href="{{ link.url }}">{{ link.title }}</a>
  
{% if link.links != blank %}
  <ul class="acnav__list acnav__list--level2">
    {% for child_link in link.links %}  
    <li class="">      
<a class="acnav__link acnav__link--level2" href="{{ child_link.url }}">{{ child_link.title }}</a>
    {% if child_link.links != blank %}
     <ul class="acnav__list acnav__list--level3">
      {% for grandchild_link in child_link.links %}  
        <li><a class="acnav__link acnav__link--level3" href= "{{ grandchild_link.url }}">{{ grandchild_link.title }}</a></li>
      {% endfor %}
      </ul>
    {% endif %}   
       
    </li>
    {% endfor %}
  </ul> 
{% endif %} 
</li>
  {% else %}
  <li class="has-children">
  <a class="toggles new-sub"  href="{{ link.url }}">{{ link.title }}</a>
  <span class="acnav__label"><svg width="14" height="9" viewBox="0 0 14 9" fill="none" xmlns="http://www.w3.org/2000/svg">
<path d="M13.9999 1.46459C14.0004 1.63536 13.9675 1.80409 13.9034 1.95838C13.8394 2.11267 13.746 2.2486 13.63 2.35618L7.63053 7.87717C7.45162 8.0453 7.22719 8.13721 6.99559 8.13721C6.76399 8.13721 6.53957 8.0453 6.36065 7.87717L0.361218 2.16186C0.157021 1.96784 0.0286086 1.68903 0.00423118 1.38678C-0.0201462 1.08452 0.061508 0.783573 0.231231 0.55014C0.400953 0.316708 0.644841 0.169911 0.909243 0.142044C1.17364 0.114176 1.4369 0.207521 1.6411 0.401542L7.00059 5.51103L12.3601 0.573002C12.5069 0.433225 12.6856 0.344435 12.8751 0.31714C13.0646 0.289844 13.257 0.325184 13.4296 0.418979C13.6021 0.512774 13.7475 0.661098 13.8485 0.8464C13.9496 1.0317 14.0022 1.24623 13.9999 1.46459Z" fill="#1C1C1C"/>
</svg>
</span>
{% if link.links != blank %}
  <ul class="acnav__list acnav__list--level2">
    {% for child_link in link.links %}  
    <li>
      
 <a class="acnav__link acnav__link--level2"href="{{ child_link.url }}">{{ child_link.title }}</a>
  </li>
    {% endfor %}
  </ul> 
{% endif %} 
</li>
  {% endif %}
{% endfor %}
</ul>
  
  </div>

<style>  
    .acnav__list--level2 {
    display: none;
  
    .is-open   {
      display: block;
    }
  }
  </style>

  <script>
    $( document ).ready(function() {
  $('.acnav__label').click(function () {
  
	var label = $(this);
	var parent = label.parent('.has-children');
	var list = label.siblings('.acnav__list');

	if ( parent.hasClass('is-open') ) {
    label.removeClass("icon-new");
		list.slideUp('200');
		parent.removeClass('is-open');
	}
	else {
     label.addClass("icon-new");
		list.slideDown('200');
		parent.addClass('is-open');
	}
});
      });
   </script>




     $(document).ready(function () {
//collection page sidebar filter 

/ when customer click on li / $("ul.collside_nav .collection-tag").each(function() {
    $(this).click(function(event) {
        event.preventDefault();
        
        // Remove active class from other li elements
        $("ul.collside_nav .collection-tag").not(this).removeClass("active_collection");
        
        // Toggle the active_collection class on the clicked li
        $(this).toggleClass("active_collection");

        var collectionurl = $(this).attr('coll_handle');
        // console.log('collectionurl', collectionurl);

        $.ajax({
            type: 'GET',
            url: collectionurl,
            data: {},
            success: function(collectiondata) {
                var pagehtml = $(collectiondata).find("#product-grid").html();
                $("#product-grid").html(pagehtml);

                if ($('#product-grid').find('.title--primary').length > 0) {
                    $('#product-grid').parents('.collection').find('.pagination-wrapper').hide();
                    $('#product-grid').parents('.collection').find('.buttons').hide();
                } else {
                    $('#product-grid').parents('.collection').find('.pagination-wrapper').show();
                    $('#product-grid').parents('.collection').find('.buttons').show();
                }
            }
        });
    });
});
//collection page sidebar filter 

/ when customer click on li / 
    
  });
