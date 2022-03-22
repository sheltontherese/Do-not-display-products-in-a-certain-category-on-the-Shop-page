# Do-not-display-products-in-a-certain-category-on-the-Shop-page
Do not display products in a certain category on the Shop page
Thay chữ shoes thành slug của category sản phẩm mà bạn cần loại bỏ, có thể thêm nhiều bằng cách điền như array( 'shoes', 'computer' ).

/**
 * Remove products from shop page by category
 *
 */
function woo_custom_pre_get_posts_query( $q ) {
 
        if ( ! $q->is_main_query() ) return;
        if ( ! $q->is_post_type_archive() ) return;
 
        if ( ! is_admin() && is_shop() ) {
 
                $q->set( 'tax_query', array(array(
                        'taxonomy' => 'product_cat',
                        'field' => 'slug',
                        'terms' => array( 'shoes' ), // Don't display products in the shoes category on the shop page
                        'operator' => 'NOT IN'
                )));
 
        }
 
        remove_action( 'pre_get_posts', 'custom_pre_get_posts_query' );
 
}
add_action( 'pre_get_posts', 'woo_custom_pre_get_posts_query' );
