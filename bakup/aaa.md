<script src="/media/js/jquery.tagcloud.js" type="text/javascript" charset="utf-8"></script> 
<script language="javascript">
$.fn.tagcloud.defaults = {
    size: {start: 1, end: 1, unit: 'em'},
      color: {start: '#999999', end: '#008000'}
};

$(function () {
    $('#tag_cloud a').tagcloud();
});
</script>
